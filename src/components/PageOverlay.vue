<script setup>
const gameBoard = defineProps([gameBoard])
</script>

<template>
<div class="overlay">
    <h1>Hallo</h1>
</div>
</template>

<style scoped>
.overlay {
    position: absolute;
    background-color: rgba(211, 211, 211, 0);
    backdrop-filter: blur(10px);
    height: 100vh;
    width: 100vw;
}
</style>