<template>
    <div class="source-controls-container">
        <!-- TODO: Put buttons in Object and use v-for to create -->
        <template v-if="hasCameraOnly && showCameraFeed && !showCaptureAndCamera">
            <div class="camera-controls controls">
                <button class="button" @click="setCameraSize(100)" :class="{ active: cameraSize == 100 }">
                    <span class="icon profile"></span>
                </button>
                <button class="button eighty-percent" @click="setCameraSize(80)" :class="{ active: cameraSize == 80 }">
                    <span class="bg">
                        <span class="icon profile"></span>
                    </span>
                </button>
                <button class="button sixty-percent" @click="setCameraSize(60)" :class="{ active: cameraSize == 60 }">
                    <span class="bg">
                        <span class="icon profile"></span>
                    </span>
                </button>
            </div>
        </template>

        <template v-else-if="hasCaptureOnly && showCaptureFeed && !showCaptureAndCamera">
            <div class="capture-controls controls">
                <button class="button active">
                    <span class="icon screenshare"></span>
                </button>
            </div>
        </template>

        <template v-else-if="hasCaptureAndCamera && showCaptureAndCamera">
            <div class="camera-capture-controls controls">
                <button class="button left" @click="setSharedLayout('left')" :class="{ active: captureAndCameraLayout === 'left' }">
                    <span class="icon screenshare"></span>
                    <span class="bg">
                        <span class="icon profile"></span>
                    </span>
                </button>
                <button class="button right" @click="setSharedLayout('right')" :class="{ active: captureAndCameraLayout === 'right' }">
                    <span class="icon screenshare"></span>
                    <span class="bg">
                        <span class="icon profile"></span>
                    </span>
                </button>
                <button class="button split" @click="setSharedLayout('split')" :class="{ active: captureAndCameraLayout === 'split' }">
                    <span class="icon screenshare"></span>
                    <span class="icon profile"></span>
                </button>
            </div>
        </template>
    </div>
</template>

<script setup>
import { inject } from 'vue';

// TODO: Create object for buttons to be created dynamically
// defineProps({
//     buttons: {
//         camera: { id: 1 },
//         capture: { id: 2 },
//         both: { id: 3 }
//     }
// });

const hasCameraOnly = inject('hasCameraOnly');
const hasCaptureOnly = inject('hasCaptureOnly');
const hasCaptureAndCamera = inject('hasCaptureAndCamera');
const showCameraFeed = inject('showCameraFeed');
const showCaptureFeed = inject('showCaptureFeed');
const showCaptureAndCamera = inject('showCaptureAndCamera');

const captureAndCameraLayout = inject('captureAndCameraLayout');
const cameraSize = inject('cameraSize');

const setSharedLayout = (type) => {
    captureAndCameraLayout.value = type;
}

const setCameraSize = (size) => {
    cameraSize.value = size;
};
</script>

<style lang="scss" scoped>
@import "../assets/scss/_variables";
@import "../assets/scss/_mixins";

.source-controls-container {
    bottom: toRem(-64);
    height: toRem(40);
    position: absolute;
    text-align: center;
    width: 100%;

    .controls {
        align-items: center;
        display: flex;
        flex-direction: row;
        flex-wrap: nowrap;
        justify-content: center;
    }

    .button {
        align-items: center;
        background: $mid-gray;
        border: none;
        border-radius: toRem(4);
        cursor: pointer;
        display: flex;
        height: toRem(40);
        justify-content: center;
        margin-right: toRem(8);
        width: toRem(60);

        &:hover,
        &:focus,
        &:active,
        &.active {
            background-color: $light-primary;
            @include box-border($primary, 4);

            .profile { background-image: url(../assets/images/icon-user.svg); }
            .screenshare { background-image: url(../assets/images/icon-media.svg); }
            .bg { background: $light-primary; }
        }

        &:last-of-type {
            margin-right: 0;
        }

        .bg {
            align-self: center;
            background: $med-gray;
            border-radius: toRem(4);
            display: flex;
            justify-content: center;
        }

        &.eighty-percent {

            .bg {
                height: toRem(27);
                width: toRem(46);
            }

            &:hover, &:focus, &:active, &.active {
                background: $white;

                .bg { background: $light-primary; }
            }
        }

        &.sixty-percent {

            .bg {
                height: toRem(20);
                width: toRem(40);
            }

            &:hover, &:focus, &:active, &.active {
                background: $white;

                .bg { background: $light-primary; }
            }
        }

        .profile {
            align-self: center;
            background: url(../assets/images/icon-user_gray.svg);
            background-position: center center;
            background-size: toRem(12) toRem(12);
            background-repeat: no-repeat;
            display: flex;
            height: toRem(12);
            justify-content: center;
            width: toRem(12);
        }

        .screenshare {
            align-self: center;
            background: url(../assets/images/icon-media_gray.svg);
            background-position: center center;
            background-size: toRem(12) toRem(12);
            background-repeat: no-repeat;
            display: flex;
            height: 100%;
            width: 100%;
        }

        &.left,
        &.right {
            position: relative;

            .screenshare {
                align-self: center;
                justify-content: center;
                position: relative;
            }

            .bg {
                background: $med-gray;
                border-radius: toRem(4);
                padding: 0 toRem(2);
                position: absolute;

                .profile {
                    background-size: toRem(6) toRem(6);
                }
            }

            &:hover,
            &:focus,
            &:active,
            &.active {
                background: $light-primary;

                .screenshare { background-image: url(../assets/images/icon-media.svg); }
                .profile { background-image: url(../assets/images/icon-user.svg); }

                .bg {
                    background: $white;
                }
            }
        }

        &.left {
            .bg {
                bottom: toRem(4);
                left: toRem(4);
            }
        }

        &.right {
            .bg {
                bottom: toRem(4);
                right: toRem(4);
            }}

        &.split {
            align-items: stretch;
            display: flex;
            flex-direction: row;
            flex-wrap: nowrap;
            justify-content: stretch;
            overflow: hidden;
            padding: 0;
            position: relative;

            .screenshare {
                height: 100%;
                position: relative;
                width: 65%;
                z-index: 1;
            }

            .profile {
                background-color: $med-gray;
                height: 100%;
                position: relative;
                width: 35%;
                z-index: 1;
            }

            &:hover,
            &:focus,
            &:active,
            &.active {
                box-shadow: none;

                .screenshare { background-image: url(../assets/images/icon-media.svg); }
                .profile {
                    background-color: $white;
                    background-image: url(../assets/images/icon-user.svg);
                }

                &:after {
                    border-radius: toRem(4);
                    bottom: 0;
                    @include box-border($primary, 4);
                    content: '';
                    left: 0;
                    position: absolute;
                    right: 0;
                    top: 0;
                    z-index: 2;
                }
            }
        }
    }
}
</style>
