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
                            <div
                                class="border-gray-200 rounded bg-gray-50 flex-auto flex justify-center items-center font-medium">
                                <div class="card flex justify-center py-10">
                                    <div class="flex flex-col gap-2">
                                        <label for="username">Username</label>
                                        <InputText id="username" v-model="Username" aria-describedby="username-help" />
                                    </div>
                                </div>
                            </div>
                        </div>
                        <div class="flex p-4 justify-end bg-gray-50 ">
                            <Button label="Next" icon="pi pi-arrow-right" iconPos="right"
                                @click="validateStep1(activateCallback)" />
                        </div>
                    </div>
                </StepPanel>

                <StepPanel v-slot="{ activateCallback }" value="2">
                    <div class="border-2 border-dashed ">
                        <div class="flex flex-col h-full ">
                            <div
                                class="border-gray-200 rounded bg-gray-50 flex-auto flex justify-center items-center font-medium">
                                <div class="card flex gap-6 items-center justify-center py-10">
                                    <Toast />
                                    <FileUpload ref="fileUploadRef" mode="basic" name="demo[]" url="/api/upload"
                                        accept=".png,.jpg,.jpeg,.pdf" :maxFileSize="1000000" @upload="onUpload"
                                        @select="onSelectedFiles" :files="files" />


                                    <!-- Conditionally render the View and Remove buttons -->
                                    <div v-if="files.length > 0" class="flex gap-2 mt-4">
                                        <Button icon="pi pi-eye" severity="info" class="rounded" @click="showPreview" />
                                        <Button icon="pi pi-times" @click="removeFile" severity="danger" />
                                    </div>
                                </div>
                            </div>
                        </div>
                        <div class="flex p-4 justify-between bg-gray-50 ">
                            <Button label="Back" severity="secondary" icon="pi pi-arrow-left"
                                @click="activateCallback('1')" />
                            <Button label="Next" icon="pi pi-arrow-right" iconPos="right"
                                @click="validateStep2(activateCallback)" />
                        </div>
                    </div>
                </StepPanel>

                <StepPanel v-slot="{ activateCallback }" value="3">
                    <div class="border-2 border-dashed">
                        <div class="flex flex-col h-full">
                            <div
                                class="border-gray-200 rounded bg-gray-50 flex-auto flex justify-center items-center font-medium">
                                <div class="card flex justify-center py-10">
                                    <div class="flex flex-col gap-2">
                                        <label for="address">ADDRESS</label>
                                        <Textarea v-model="address" rows="5" cols="30" />
                                    </div>
                                </div>
                            </div>
                        </div>
                        <div class="p-4 bg-gray-50 ">
                            <Button label="Back" severity="secondary" icon="pi pi-arrow-left"
                                @click="activateCallback('2')" />
                        </div>
                    </div>
                </StepPanel>
            </StepPanels>
        </Stepper>
    </div>
    <Dialog v-model:visible="previewVisible" header="File Preview" :style="{ width: '50rem' }">
        <div v-for="file in files" :key="file.name" class="mb-4">
 
    <div v-if="file && (file.type === 'image/png'|| file.type === 'image/jpeg')">
        <img :src="file.objectURL" alt="Preview" class="w-full h-auto" />
    </div>

    <!-- Check for PDF type and display PDF preview -->
    <div v-else-if="file && file.type === 'application/pdf'">
        <iframe :src="file.objectURL" class="w-full h-96" frameborder="0"></iframe>
    </div>

    <!-- Show a message if file type is unsupported -->
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


const fileUploadRef = ref(null); // Create a ref for FileUpload

const toast = useToast();


const previewVisible = ref(false);


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
    debugger
    files.value = event.files.map((file) => {
    console.log('File selected:', file); // Log file details

    return {
        ...file, 
        name:file.name,
        type:file.type,
        objectURL: URL.createObjectURL(file) // Create a URL for preview
    };
});
};




const removeFile = () => {
    // Clear the files array
    files.value = [];

    // Clear the FileUpload component using the ref
    if (fileUploadRef.value) {
        fileUploadRef.value.clear();
    }

    // Show a success message
    toast.add({ severity: 'info', summary: 'Success', detail: 'Files removed successfully', life: 3000 });
};
const getFileType = (file) => {
   console.log(file,"getFileType")
    if (file && file.name) {
        // Check if file has a type property and return it if available
        if (file.type) {
            return file.type;
        }

        // If type is undefined, fallback to checking the file extension
        const extension = file.name.split('.').pop().toLowerCase();
        if (['png', 'jpg', 'jpeg'].includes(extension)) {
            return 'image/' + extension;  // Return 'image/png', 'image/jpg', etc.
        } else if (extension === 'pdf') {
            return 'application/pdf';  // Return 'application/pdf'
        }
    }

    return 'unknown';  // If file or file.name is undefined, return 'unknown'
};


const showPreview = () => {
    previewVisible.value = true; // Show the preview dialog
};

const closePreview = () => {
    previewVisible.value = false; // Hide the preview dialog
};
</script>
