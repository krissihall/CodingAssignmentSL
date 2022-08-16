<template>
    <template v-if="showCameraFeed && !showCaptureFeed">
        <div class="camera-item-container" :class="cameraSizeClass">
            <img src="../assets/images/camera.jpg" class="img-responsive" alt="Camera placeholder image" />
        </div>
    </template>
</template>

<script setup>
import { inject, computed } from 'vue';

const hasCaptureAndCamera = inject('hasCaptureAndCamera');
const showCameraFeed = inject('showCameraFeed');
const showCaptureFeed = inject('showCaptureFeed');
const cameraSize = inject('cameraSize');

const cameraSizeClass = computed(() => {
    if (cameraSize.value === 80) {
        return 'eighty';
    } else if (cameraSize.value === 60) {
        return 'sixty';
    } else {
        return;
    }
});
</script>

<style lang="scss" scoped>
@import "../assets/scss/_variables";
@import "../assets/scss/_mixins";

.camera-item-container {
    align-items: center;
    background: $black;
    display: flex;
    height: 100%;
    justify-content: center;
    position: absolute;
    width: 100%;
    z-index: 2;

    &.eighty {
        margin: 0 10%;
        width: 80%;
    }

    &.sixty {
        margin: 0 20%;
        width: 60%;
    }

    .img-responsive {
        height: 100%;
        object-fit: contain;
        width: 100%;
    }
}
</style>
