<template>
    <div class="source-container">
        <button class="btn btn-primary" @click="addMediaSource">Add Source</button>

        <!-- TODO: Make this dynamic using v-for -->
        <template v-if="hasMediaSourceAdded">
            <template v-if="hasCameraOnly">
                <div class="media-source camera-media-source">
                    <button class="btn btn-sm" :class="btnClassCameraFeed" @click="toggleCameraFeed">{{btnTextCameraFeed}} on stream</button>
                    <span class="label">My video feed</span>
                </div>
            </template>

            <template v-if="hasCaptureOnly">
                <div class="media-source capture-media-source">
                    <button class="btn btn-sm" :class="btnClassCaptureFeed" @click="toggleCaptureFeed">{{btnTextCaptureFeed}} on stream</button>
                    <span class="label">My screen feed</span>
                </div>
            </template>
        </template>

        <template v-else>
            <button class="btn btn-secondary btn-lg add-media-source" @click="addMediaSource">
                <span class="plus-icon"></span>
                <span class="h3">Add media source</span>
                <span class="p">Screenshare, Camera</span>
            </button>
        </template>
    </div>
    
    <template v-if="showMediaModal">
        <media-modal></media-modal>
    </template>
</template>

<script setup>
import { inject, computed, ref } from 'vue';
import MediaModal from './MediaModal.vue';

const hasCameraOnly = inject('hasCameraOnly');
const hasCaptureOnly = inject('hasCaptureOnly');

const showMediaModal = inject('showMediaModal');
const hasMediaSourceAdded = inject('hasMediaSourceAdded');
const showCameraFeed = inject('showCameraFeed');
const showCaptureFeed = inject('showCaptureFeed');

const btnTextCameraFeed = ref('Show');
const btnClassCameraFeed = ref('btn-primary')
const btnTextCaptureFeed = ref('Show');
const btnClassCaptureFeed = ref('btn-primary');

const addMediaSource = () => {
    if (!showMediaModal.value) {
        showMediaModal.value = true;
    }
};

const toggleCameraFeed = () => {
    if (!showCameraFeed.value) {
        showCameraFeed.value = true;
        btnTextCameraFeed.value = 'Hide';
        btnClassCameraFeed.value = 'btn-danger';
    } else {
        showCameraFeed.value = false;
        btnTextCameraFeed.value = 'Show';
        btnClassCameraFeed.value = 'btn-primary'
    }
};

const toggleCaptureFeed = () => {
    if (!showCaptureFeed.value) {
        showCaptureFeed.value = true;
        btnTextCaptureFeed.value = 'Hide';
        btnClassCaptureFeed.value = 'btn-danger';
    } else {
        showCaptureFeed.value = false;
        btnTextCaptureFeed.value = 'Show';
        btnClassCaptureFeed.value = 'btn-primary';
    }
};
</script>

<style lang="scss" scoped>
@import "../assets/scss/_variables";
@import "../assets/scss/_mixins";

.source-container {
    align-self: start;
    box-sizing: border-box;
    border-right: toRem(1) solid $mid-gray;
    flex-direction: column;
    flex-wrap: nowrap;
    height: 100%;
    padding: toRem(16);
    width: auto;

    .media-source {
        align-items: center;
        aspect-ratio: 16 / 9;
        border-radius: toRem(4);
        display: flex;
        flex-direction: column;
        flex-wrap: nowrap;
        justify-content: center;
        margin-top: toRem(16);
        overflow: hidden;
        position: relative;

        .label {
            bottom: toRem(4);
            color: $white;
            left: toRem(8);
            font-size: toRem(13);
            position: absolute;
            z-index: 3;
        }

        &.camera-media-source {
            background: url(../assets/images/camera.jpg);
            background-position: center center;
            background-size: cover;
            background-repeat: no-repeat;
        }

        &.capture-media-source {
            background: url(../assets/images/capture.jpg);
            background-position: center center;
            background-size: cover;
            background-repeat: no-repeat;
        }

        &:after {
            background: linear-gradient(0deg, rgba($black, 1) 0%, rgba($black, 0) 100%);
            bottom: 0;
            content: '';
            height: toRem(24);
            left: 0;
            opacity: 0.8;
            position: absolute;
            right: 0;
            z-index: 2;
        }
    }

    .add-media-source {
        align-items: center;
        display: flex;
        flex-direction: column;
        @include default-font;
        justify-content: center;
        margin-top: toRem(16);

        .plus-icon {
            background-image: url('../assets/images/icon-plus.svg');
            background-position: center center;
            background-repeat: no-repeat;
            background-size: toRem(14) toRem(14);
            height: toRem(16);
            margin-bottom: toRem(8);
            margin-top: toRem(16);
            width: toRem(16);
        }

        .h3 {
            @include bold-font;
            margin-bottom: toRem(4);
        }

        .p {
            font-size: toRem(14);
        }
    }
}
</style>
