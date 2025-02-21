<template>
    <div class="card flex justify-center">
        <Stepper value="1" class="basis-[50rem]">
            <StepList>
                <Step value="1">Step 1</Step>
                <Step value="2">Step 2</Step>
                <Step value="3">Step 3</Step>
            </StepList>
            <StepPanels>
                <StepPanel v-slot="{ activateCallback }" value="1">
                    <div class="border-2 border-dashed">
                    <div class="flex flex-col h-full">
                        <div class=" border-gray-200  rounded bg-gray-50  flex-auto flex justify-center items-center font-medium">
                            <div class="card flex justify-center py-10">
                                <div class="flex flex-col gap-2">
                                    <label for="username">Username</label>
                                    <InputText id="username" v-model="Username" aria-describedby="username-help" />
                              
                                </div>
                            </div>
                        </div>
                    </div>
                    <div class="flex p-4 justify-end bg-gray-50 ">
                        <Button label="Next" icon="pi pi-arrow-right" iconPos="right" @click="validateStep1(activateCallback)" />
                    </div>
                </div>
                </StepPanel>

                <StepPanel v-slot="{ activateCallback }" value="2">
                    <div class="border-2 border-dashed">
                    <div class="flex flex-col h-full">
                        <div class=" border-gray-200  rounded bg-gray-50  flex-auto flex justify-center items-center font-medium">
                            <div class="card py-10">
                                <Toast />
                                <FileUpload name="demo[]" url="/api/upload" @upload="onTemplatedUpload" :multiple="true" accept="image/*" :maxFileSize="1000000" @select="onSelectedFiles">
                                    <template #header="{ chooseCallback, uploadCallback, clearCallback, files }">
                                        <div class="gap-">
                                            <div class="flex gap-2">
                                                <Button @click="chooseCallback()" icon="pi pi-images" rounded outlined severity="secondary"></Button>
                                            </div>
                                        </div>
                                    </template>
                                    <template #content="{ files, uploadedFiles, removeUploadedFileCallback, removeFileCallback }">
                                        <div class="flex flex-col gap-4 pt-1">
                                            <div v-if="files.length > 0">
                                                <h5>Files to Upload</h5>
                                                <div class="flex flex-wrap gap-2">
                                                    <div v-for="(file, index) of files" :key="file.name + file.type + file.size" class="p-8 rounded-border flex flex-col border border-gray items-center gap-4">
                                                        <div>
                                                            <img role="presentation" :alt="file.name" :src="file.objectURL" width="70" height="30" />
                                                        </div>
                                                        <span class="font-semibold text-ellipsis max-w-60 whitespace-nowrap overflow-hidden">{{ file.name }}</span>
                                                        <div>{{ formatSize(file.size) }}</div>
                                                        <Button icon="pi pi-times" @click="onRemoveTemplatingFile(file, removeFileCallback, index)" outlined rounded severity="danger" />
                                                    </div>
                                                </div>
                                            </div>

                                            <div v-if="uploadedFiles.length > 0">
                                                <h5>Completed</h5>
                                                <div class="flex flex-wrap gap-2">
                                                    <div v-for="(file, index) of uploadedFiles" :key="file.name + file.type + file.size" class="p-8 rounded-border flex flex-col border border-gray items-center gap-4">
                                                        <div>
                                                            <img role="presentation" :alt="file.name" :src="file.objectURL" width="100" height="50" />
                                                        </div>
                                                        <span class="font-semibold text-ellipsis max-w-60 whitespace-nowrap overflow-hidden">{{ file.name }}</span>
                                                        <div>{{ formatSize(file.size) }}</div>
                                                        <Badge value="Completed" class="mt-4" severity="success" />
                                                        <Button icon="pi pi-times" @click="removeUploadedFileCallback(index)" outlined rounded severity="danger" />
                                                    </div>
                                                </div>
                                            </div>
                                        </div>
                                    </template>
                                    <template #empty>
                                        <div class="flex items-center justify-center flex-col">
                                            <i class="pi pi-cloud-upload !border-2 !rounded-full !p-5 !text-4xl !text-muted-color" />
                                            <p class="mt-6 mb-0">Drag and drop files to here to upload.</p>
                                        </div>
                                    </template>
                                </FileUpload>
                            </div>
                        </div>
                    </div>
                    <div class="flex p-4 justify-between bg-gray-50 ">
                        <Button label="Back" severity="secondary" icon="pi pi-arrow-left" @click="activateCallback('1')" />
                        <Button label="Next" icon="pi pi-arrow-right" iconPos="right" @click="validateStep2(activateCallback)" />
                    </div>
                </div>
                </StepPanel>

                <StepPanel v-slot="{ activateCallback }" value="3">
                    <div class="border-2 border-dashed">
                    <div class="flex flex-col h-full">
                        <div class="
                         border-gray-200  rounded bg-gray-50  flex-auto flex justify-center items-center font-medium">
                            <div class="card flex justify-center py-10">
                                <div class="flex flex-col gap-2">
                                    <label for="username">ADDRESS</label>
                                    <Textarea v-model="value" rows="5" cols="30" />
                                
                                </div>
                            </div>
                        </div>
                    </div>
                    <div class="p-4 bg-gray-50 ">
                        <Button label="Back" severity="secondary" icon="pi pi-arrow-left" @click="activateCallback('2')" />
                    </div>
                    </div>
                </StepPanel>
            </StepPanels>
        </Stepper>
    </div>
</template>

<script setup>
import { ref } from 'vue';
import { usePrimeVue } from 'primevue/config';
import { useToast } from 'primevue/usetoast';

const Username = ref(null);
const address = ref(null);
const files = ref([]);
const uploadedFiles = ref([]);
const totalSize = ref(0);
const totalSizePercent = ref(0);
const $primevue = usePrimeVue();
const toast = useToast();

const formatSize = (bytes) => {
    const k = 1024;
    const dm = 3;
    const sizes = $primevue.config.locale.fileSizeTypes;

    if (bytes === 0) {
        return `0 ${sizes[0]}`;
    }

    const i = Math.floor(Math.log(bytes) / Math.log(k));
    const formattedSize = parseFloat((bytes / Math.pow(k, i)).toFixed(dm));

    return `${formattedSize} ${sizes[i]}`;
};

// Step 1 Validation
const validateStep1 = (activateCallback) => {
    if (!Username.value) {
        toast.add({ severity: 'error', summary: 'Error', detail: 'Please enter a username.', life: 3000 });
    } else {
        activateCallback('2');
    }
};

// Step 2 Validation
const validateStep2 = (activateCallback) => {
    // Check if files are empty after removing any files
    if (files.value.length === 0) {
        toast.add({ severity: 'error', summary: 'Error', detail: 'Please upload at least one file.', life: 3000 });
    } else {
        activateCallback('3');
    }
};

// File Upload Methods
const onRemoveTemplatingFile = (file, removeFileCallback, index) => {
    removeFileCallback(index);
    // Manually re-check files after removal
    if (files.value.length === 0) {
        toast.add({ severity: 'error', summary: 'Error', detail: 'Please upload at least one file.', life: 3000 });
    }
    files.value=[];
    totalSize.value -= parseInt(formatSize(file.size));
    totalSizePercent.value = totalSize.value / 10;
};

const onSelectedFiles = (event) => {
    files.value = event.files.map((file) => ({
        ...file,
    }));
    files.value.forEach((file) => {
        totalSize.value += parseInt(formatSize(file.size));
    });
};

const onTemplatedUpload = () => {
    uploadedFiles.value = [...uploadedFiles.value, ...files.value];
    files.value = [];
    toast.add({ severity: 'info', summary: 'Success', detail: 'Files uploaded', life: 3000 });
};

</script>
