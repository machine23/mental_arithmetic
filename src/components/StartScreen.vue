<template>
    <div class="container">
        <h1>Are you ready?</h1>
        <button @click="$emit('onStart')">Start</button>
    </div>
</template>

<script>
export default {}
</script>

<style scoped>
.container {
    width: 650px;
    text-align: center;
    margin: 0 auto;
}
</style>
