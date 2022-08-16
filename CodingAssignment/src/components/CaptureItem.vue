<template>
    <template v-if="showCaptureFeed && !showCameraFeed">
        <div class="source-item-container">
            <img src="../assets/images/capture.jpg" class="img-responsive" alt="Screen capture placeholder image" />
        </div>
    </template>
</template>

<script setup>
import { inject } from 'vue';

const hasCaptureAndCamera = inject('hasCaptureAndCamera');
const showCaptureFeed = inject('showCaptureFeed');
const showCameraFeed = inject('showCameraFeed');
</script>

<style lang="scss" scoped>
@import "../assets/scss/_variables";
@import "../assets/scss/_mixins";

.source-item-container {
    align-items: center;
    background: $black;
    display: flex;
    height: 100%;
    justify-content: center;
    position: absolute;
    width: 100%;
    z-index: 2;

    .img-responsive {
        height: 100%;
        object-fit: contain;
        width: 100%;
    }
}
</style>
