<script setup>
const props = defineProps(['placeholder'])

</script>

<template>
    <div class="image">
        <img :src="props.placeholder" class="w-full">
    </div>
</template>

<style scoped>
</style>
