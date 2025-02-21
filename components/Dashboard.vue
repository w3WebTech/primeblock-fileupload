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
                            <div class="border-gray-200 rounded bg-gray-50 flex-auto flex justify-center items-center font-medium">
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
                    <div class="border-2 border-dashed ">
                        <div class="flex flex-col h-full ">
                            <div class="border-gray-200 rounded bg-gray-50 flex-auto flex justify-center items-center font-medium">
                                <div class="card flex gap-6 items-center justify-center py-10">
                                    <Toast />
                                    <FileUpload
                                        ref="fileupload"
                                        mode="basic"
                                        name="demo[]"
                                        url="/api/upload"
                                        accept=".png,.jpg,.jpeg,.pdf"
                                        :maxFileSize="1000000"
                                        @upload="onUpload"
                                        @select="onSelectedFiles"
                                        :files="files"
                                    />
                                    
                                    <!-- Conditionally render the View and Remove buttons -->
                                    <div v-if="files.length > 0" class="flex gap-2 mt-4">
                                        <Button icon="pi pi-eye" severity="info" class="rounded" @click="showPreview" />
                                        <Button icon="pi pi-times" @click="removeFile" severity="danger" />
                                    </div>
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
                            <div class="border-gray-200 rounded bg-gray-50 flex-auto flex justify-center items-center font-medium">
                                <div class="card flex justify-center py-10">
                                    <div class="flex flex-col gap-2">
                                        <label for="address">ADDRESS</label>
                                        <Textarea v-model="address" rows="5" cols="30" />
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

    <Dialog v-model:visible="previewVisible" header="File Preview" :style="{ width: '50rem' }">
        <div v-for="file in files" :key="file.name" class="mb-4">
            <div v-if="file && file.type && file.type.startsWith('image/')">
                <img :src="file.objectURL" alt="Preview" class="w-full h-auto" />
            </div>
            <div v-else-if="file && file.type === 'application/pdf'">
                <iframe :src="file.objectURL" class="w-full h-96" frameborder="0"></iframe>
            </div>
            <div v-else>
                <p>Unsupported file type: {{ file.name }}</p>
            </div>
        </div>
        <div class="flex justify-end">
            <Button label="Close" @click="closePreview" />
        </div>
    </Dialog>
</template>

<script setup>
import { ref } from 'vue';
import { usePrimeVue } from 'primevue/config';
import { useToast } from 'primevue/usetoast';
import Toast from 'primevue/toast';
import FileUpload from 'primevue/fileupload';
import Button from 'primevue/button';
import InputText from 'primevue/inputtext';
import Textarea from 'primevue/textarea';
import Stepper from 'primevue/stepper';
import Step from 'primevue/step';
import StepList from 'primevue/steplist';
import StepPanel from 'primevue/steppanel';

const Username = ref(null);
const address = ref(null);
const files = ref([]);
const uploadedFiles = ref([]);
const totalSize = ref(0);
const totalSizePercent = ref(0);
const $primevue = usePrimeVue();
const toast = useToast();

const visible = ref(false);
const previewVisible = ref(false);

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

const validateStep1 = (activateCallback) => {
    if (!Username.value) {
        toast.add({ severity: 'error', summary: 'Error', detail: 'Please enter a username.', life: 3000 });
    } else {
        activateCallback('2');
    }
};

const validateStep2 = (activateCallback) => {
    if (files.value.length === 0) {
        toast.add({ severity: 'error', summary: 'Error', detail: 'Please upload at least one file.', life: 3000 });
    } else {
        activateCallback('3');
    }
};

const onSelectedFiles = (event) => {
    files.value = event.files.map((file) => ({
        ...file,
        objectURL: URL.createObjectURL(file) // Create a URL for preview
    }));
};

const removeFile = () => {
    files.value = []; // Clear the files array
    $refs.fileupload.clear(); // Clear the FileUpload component
    toast.add({ severity: 'info', summary: 'Success', detail: 'Files removed successfully', life: 3000 });
};

const showPreview = () => {
    previewVisible.value = true; // Show the preview dialog
};

const closePreview = () => {
    previewVisible.value = false; // Hide the preview dialog
};

</script>