<template>
    <div class="main-controls-container">
        <div class="button-controls">
            <button class="btn btn-secondary">Chat</button>
            <button class="btn btn-secondary">Record</button>
            <button class="btn btn-primary">Go Live</button>
        </div>
    </div>
</template>

<script setup>
</script>

<style lang="scss" scoped>
@import "../assets/scss/_variables";
@import "../assets/scss/_mixins";

.main-controls-container {
    bottom: 0;
    display: flex;
    justify-content: center;
    position: fixed;
    width: 100%;
}

.button-controls {
    border: toRem(2) solid $mid-gray;
    border-top-left-radius: toRem(12);
    border-top-right-radius: toRem(12);
    padding: toRem(8);
    width: auto;

    .btn {
        margin-right: toRem(8);

        &:last-of-type {
            margin-right: 0;
        }
    }
}
</style>
