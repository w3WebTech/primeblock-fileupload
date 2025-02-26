<template>
  <div class="card flex justify-center">
    <Stepper value="1" class="basis-[50rem]">
      <StepList>
        <Step value="1">Step 1</Step>
        <Step value="2">Step 2</Step>
        <Step value="3">Step 3</Step>
      </StepList>
      <StepPanels>
        <!-- Step 1 Panel -->
        <StepPanel v-slot="{ activateCallback }" value="1">
          <div class="border-2 border-dashed">
            <div class="flex flex-col h-full">
              <div class="border-gray-200 rounded bg-gray-50 flex-auto flex justify-center items-center font-medium">
                <div class="card flex justify-center py-10">
                  <div class="flex flex-col gap-2">
                    <label for="username">Username</label>
                    <InputText
                      id="username"
                      v-model="Username"
                      aria-describedby="username-help"
                      :class="{'p-invalid': usernameErrorMessage}" 
                    />
                    <Message v-if="usernameErrorMessage" severity="error" class="mt-2 text-xs">
                      {{ usernameErrorMessage }}
                    </Message>
                  </div>
                </div>
              </div>
            </div>
            <div class=" mt-4">
      <Button label="Access Camera" @click="startCamera" />
      <Button label="Capture Image" @click="captureImage" v-if="isCameraActive" />
    </div>

    <div v-if="coordinates" class="mt-4">
      <p>Latitude: {{ coordinates.latitude }}</p>
      <p>Longitude: {{ coordinates.longitude }}</p>
    </div>
            <div class="flex p-4 justify-end bg-gray-50">
              <Button label="Next" icon="pi pi-arrow-right" iconPos="right" @click="validateStep1(activateCallback)" />
            </div>
          </div>
        </StepPanel>

        <!-- Step 2 Panel -->
        <StepPanel v-slot="{ activateCallback }" value="2">
          <div class="border-2 border-dashed">
            <div class="flex flex-col h-full">
              <div class="border-gray-200 rounded bg-gray-50 flex-auto flex justify-center items-center font-medium">
                <div class="card flex gap-6 items-center justify-center py-10">
                  <Toast />
                  <div>
                    <FileUpload
                      ref="fileUploadRef"
                      mode="basic"
                      name="demo[]"
                      url="/api/upload"
                      accept=".png,.jpg,.jpeg,.pdf"
                      :maxFileSize="5250000"
                      @upload="onUpload"
                      @select="onSelectedFiles"
                      :files="files"
                    />
                    <Message v-if="fileErrorMessage" severity="danger" class="my-5 px-5 text-red-500 text-xs">
                      {{ fileErrorMessage }}
                    </Message>
                  </div>
                  <div v-if="files.length > 0" class="flex gap-2 mt-4">
                    <Button icon="pi pi-eye" severity="info" class="rounded" @click="showPreview" />
                    <Button icon="pi pi-times" @click="removeFile" severity="danger" />
                  </div>
                </div>
              </div>
            </div>
            <div class="flex p-4 justify-between bg-gray-50">
              <Button label="Back" severity="secondary" icon="pi pi-arrow-left" @click="activateCallback('1')" />
              <Button label="Next" icon="pi pi-arrow-right" iconPos="right" @click="validateStep2(activateCallback)" />
            </div>
          </div>
        </StepPanel>

        <!-- Step 3 Panel -->
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
            <div class="p-4 bg-gray-50">
              <Button label="Back" severity="secondary" icon="pi pi-arrow-left" @click="activateCallback('2')" />
            </div>
          </div>
        </StepPanel>
      </StepPanels>
    </Stepper>

    <!-- Camera Access -->


    <Dialog v-model:visible="previewVisible" header="File Preview" :style="{ width: '50rem' }">
      <div v-for="file in files" :key="file.name" class="mb-4">
        <div v-if="file && (file.type === 'image/png' || file.type === 'image/jpeg')">
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

    <!-- Video Element for Camera -->
    <div v-if="isCameraActive" class="mt-4">
      <video ref="video" autoplay playsinline class="w-full h-auto"></video>
      <img v-if="capturedImage" :src="capturedImage" alt="Captured Image" class="mt-4 w-full h-auto" />
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
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
import Message from 'primevue/message';

const Username = ref(null);
const address = ref(null);
const files = ref([]);
const previewVisible = ref(false);
const fileErrorMessage = ref(null);
const usernameErrorMessage = ref(null);
const coordinates = ref(null);
const fileUploadRef = ref(null);
const toast = useToast();
const isCameraActive = ref(false);
const capturedImage = ref(null);

const validateStep1 = (activateCallback) => {
  if (!Username.value) {
    usernameErrorMessage.value = 'Username is required.';
  } else {
    usernameErrorMessage.value = null;
    activateCallback('2');
  }
};

const validateStep2 = (activateCallback) => {
  if (files.value.length === 0) {
    fileErrorMessage.value = 'Please upload at least one file.';
  } else {
    fileErrorMessage.value = null;
    activateCallback('3');
  }
};

const onSelectedFiles = (event) => {
  if (files.value) {
    fileErrorMessage.value = '';
  }
  files.value = event.files.map((file) => {
    return {
      ...file,
      name: file.name,
      type: file.type,
      objectURL: URL.createObjectURL(file),
    };
  });
};

const removeFile = () => {
  files.value = [];
  if (fileUploadRef.value) {
    fileUploadRef.value.clear();
  }
  toast.add({ severity: 'info', summary: 'Success', detail: 'Files removed successfully', life: 3000 });
};

const showPreview = () => {
  previewVisible.value = true;
};

const closePreview = () => {
  previewVisible.value = false;
};

const startCamera = async () => {
  try {
    const stream = await navigator.mediaDevices.getUserMedia({ video: true });
    const video = document.querySelector('video');
    video.srcObject = stream;
    isCameraActive.value = true;
  } catch (error) {
    console.error("Error accessing camera:", error);
  }
};

const captureImage = () => {
  const video = document.querySelector('video');
  const canvas = document.createElement('canvas');
  canvas.width = video.videoWidth;
  canvas.height = video.videoHeight;
  const context = canvas.getContext('2d');
  context.drawImage(video, 0, 0, canvas.width, canvas.height);
  capturedImage.value = canvas.toDataURL('image/png');
};

const getLocation = () => {
  if (navigator.geolocation) {
    navigator.geolocation.getCurrentPosition((position) => {
      coordinates.value = {
        latitude: position.coords.latitude,
        longitude: position.coords.longitude,
      };
    }, (error) => {
      console.error("Error getting location:", error);
    });
  } else {
    alert("Geolocation is not supported by this browser.");
  }
};

// Automatically request camera and location access when the component is mounted
onMounted(() => {
  getLocation();
});
</script>