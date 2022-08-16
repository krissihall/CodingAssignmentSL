<template>
  <div class="main-container">
    <sources></sources>
    <videos></videos>
  </div>

  <main-controls></main-controls>
</template>

<script setup>
import { ref, computed, provide } from 'vue';
import MainControls from './components/MainControls.vue';
import Sources from './components/Sources.vue';
import Videos from './components/Videos.vue';

const showMediaModal = ref(false);
const hasCameraOnly = ref(false);
const hasCaptureOnly = ref(false);

const showCameraFeed = ref(false);
const showCaptureFeed = ref(false);

const showCaptureAndCamera = computed(() => {
    return showCameraFeed.value && showCaptureFeed.value;
});

const hasCaptureAndCamera = computed(() => {
    return hasCameraOnly.value && hasCaptureOnly.value;
});

const hasMediaSourceAdded = computed(() => {
    return hasCameraOnly.value || hasCaptureOnly.value;
});

provide('showMediaModal', showMediaModal);
provide('hasCameraOnly', hasCameraOnly);
provide('hasCaptureOnly', hasCaptureOnly);
provide('showCameraFeed', showCameraFeed);
provide('showCaptureFeed', showCaptureFeed);
provide('showCaptureAndCamera', showCaptureAndCamera);
provide('hasCaptureAndCamera', hasCaptureAndCamera);
provide('hasMediaSourceAdded', hasMediaSourceAdded);
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Source+Sans+Pro:wght@300;400;600;700&display=swap');
@import "assets/main.scss";
</style>
