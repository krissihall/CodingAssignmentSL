<template>
    <template v-if="hasCaptureAndCamera && showCaptureAndCamera">
        <div class="center">
            <div class="capture-camera-container" :class="captureAndCameraLayout">
                <div class="capture-container">
                    <img src="../assets/images/capture.jpg" class="img-responsive" alt="Screenshare placeholder image" />
                </div>

                <div class="camera-container">
                    <img src="../assets/images/camera.jpg" class="img-responsive" alt="Camera placeholder image" />
                </div>
            </div>
        </div>
    </template>
</template>

<script setup>
import { inject } from 'vue';

const hasCaptureAndCamera = inject('hasCaptureAndCamera');
const showCaptureAndCamera = inject('showCaptureAndCamera');
const captureAndCameraLayout = inject('captureAndCameraLayout');
</script>

<style lang="scss" scoped>
@import "../assets/scss/_variables";
@import "../assets/scss/_mixins";

.capture-camera-container {
    align-items: center;
    background: $black;
    display: flex;
    height: 100%;
    justify-content: center;
    position: absolute;
    width: 100%;
    z-index: 2;

    &.left,
    &.right {

        .capture-container {
            position: relative;
            width: 100%;
            z-index: 1;
        }

        .camera-container {
            aspect-ratio: 16 / 9;
            position: absolute;
            max-width: toRem(240);
            width: 20%;
            z-index: 2;
        }
    }

    &.left {

        .camera-container {
            bottom: toRem(24);
            left: toRem(24);
        }
    }

    &.right {

        .camera-container {
            bottom: toRem(24);
            right: toRem(24);
        }
    }

    &.split {
        align-items: stretch;
        display: flex;
        flex-direction: row;
        flex-wrap: nowrap;
        height: auto;

        .capture-container {
            align-self: stretch;
            flex-grow: 3;
        }

        .camera-container {
            align-self: stretch;
            background-color: $dark;
            flex-grow: 1;
            justify-content: center;
            max-width: 20%;
            overflow: hidden;
            padding-left: toRem(16);
            position: relative;

            .img-responsive {
                object-fit: cover;
            }
        }
    }

    .img-responsive {
        height: 100%;
        object-fit: contain;
        width: 100%;
    }
}

.center {
    align-items: center;
    display: flex;
    height: 100%;
    width: 100%;
}
</style>
