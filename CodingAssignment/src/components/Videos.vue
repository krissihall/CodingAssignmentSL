<template>
    <div class="videos-container">
        <div class="video">
            <camera-item></camera-item>
            <capture-item></capture-item>
            <capture-and-camera></capture-and-camera>
            <source-controls></source-controls>
        </div>
    </div>
</template>

<script setup>
import { ref, provide } from 'vue';
import CaptureItem from './CaptureItem.vue';
import CameraItem from './CameraItem.vue';
import CaptureAndCamera from './CaptureAndCamera.vue';
import SourceControls from './SourceControls.vue';

const captureAndCameraLayout = ref('right');
const cameraSize = ref(100);

provide('captureAndCameraLayout', captureAndCameraLayout);
provide('cameraSize', cameraSize);
</script>

<style lang="scss" scoped>
@import "../assets/scss/_variables";
@import "../assets/scss/_mixins";

.videos-container {
    align-items: center;
    box-sizing: border-box;
    display: flex;
    height: 100%;
    justify-content: center;
    padding: toRem(64);
    width: auto;

    .video {
        align-items: center;
        aspect-ratio: 16 / 9;
        background: $black;
        justify-content: center;
        position: relative;
        width: 100%;
        z-index: 1;
    }
}
</style>