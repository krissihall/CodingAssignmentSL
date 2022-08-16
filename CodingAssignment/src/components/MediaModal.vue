<template>
    <!-- TODO: use transition to animate this Modal in and out -->
    <div class="modal">
        <div class="modal-content">
            <div class="modal-header">
                <h2 class="text-center">Add a new media source</h2>
            </div>

            <div class="modal-body">
                <div class="media-sources">
                    <div class="media-source" @click="addCaptureFeed">
                        <h3 class="text-center">Screenshare</h3>
                        <p class="text-center">
                            Share your entire screen, window or specific Chrome tab.
                        </p>
                    </div>

                    <div class="media-source" @click="addCameraFeed">
                        <h3 class="text-center">Video Feed</h3>
                        <p class="text-center">
                            Share a feed of your in-built webcame and microphone. If
                            you do not have a webcam, you can use a "virtual" webcam
                            such as Streamlabs Desktop virtual camera.
                        </p>
                    </div>
                </div>

                <div v-show="hasErrors" class="errors-container text-center">
                    <template v-if="showCaptureError">
                        <p class="error-msg">You already have a screenshare added.</p>
                    </template>

                    <template v-if="showCameraError">
                        <p class="error-msg">You already have a camera feed added.</p>
                    </template>

                    <button class="btn btn-primary close-btn" @click="closeModal">Close Modal</button>
                </div>
            </div>
        </div>
    </div>
    <div class="modal-backdrop"></div>
</template>

<script setup>
import { inject, computed, ref } from 'vue';

const showMediaModal = inject('showMediaModal');
const hasCameraOnly = inject('hasCameraOnly');
const hasCaptureOnly = inject('hasCaptureOnly');

const showCaptureError = ref(false);
const showCameraError = ref(false);
const hasErrors = computed(() => {
    return showCaptureError.value || showCameraError.value;
})

const addCaptureFeed = () => {
    if (hasCaptureOnly.value) {
        showCaptureError.value = true;
    } else {
        hasCaptureOnly.value = true;
        showMediaModal.value = false;
    }
};

const addCameraFeed = () => {
    if (hasCameraOnly.value) {
        showCameraError.value = true;
    } else {
        hasCameraOnly.value = true;
        showMediaModal.value = false;
    }
};

const closeModal = () => {
    showMediaModal.value = false;
};
</script>

<style lang="scss" scoped>
@import "../assets/scss/_variables";
@import "../assets/scss/_mixins";

.modal {
    align-items: center;
    bottom: 0;
    display: flex;
    left: 0;
    justify-content: center;
    position: fixed;
    right: 0;
    top: 0;
    z-index: 1001;

    .modal-content {
        align-items: center;
        background: $white;
        border-radius: toRem(8);
        box-shadow: 0 0 toRem(16) 0 rgba($black, 0.3);
        box-sizing: border-box;
        display: flex;
        flex-direction: column;
        flex-wrap: nowrap;
        height: auto;
        max-width: toRem(600);
        padding: toRem(40);
        width: 50%;
    }

    .modal-header {
        padding-bottom: toRem(40);
        width: 100%;
    }

    .modal-body {
        flex-direction: row;
        width: 100%;
    }

    .media-sources {
        box-sizing: border-box;
        column-gap: toRem(32);
        display: grid;
        grid-template-columns: auto auto;

        .media-source {
            align-self: stretch;
            background: $light-gray;
            border-radius: toRem(4);
            cursor: pointer;
            display: flex;
            flex-direction: column;
            justify-content: stretch;
            padding: toRem(32);
            transition: background 0.5s ease;

            &:hover,
            &:focus,
            &:active {
                background: darken($light-gray, 3%);
            }
        }
    }
}

.errors-container {
    margin-top: toRem(32);
}

.close-btn {
    margin-top: toRem(16);
}

.modal-backdrop {
    background: rgba(255, 255, 255, 0.6);
    bottom: 0;
    left: 0;
    position: fixed;
    right: 0;
    top: 0;
    z-index: 1000;
}
</style>
