<script setup>
const props = defineProps(["mergeImages"]);

function onClick() {
    props.mergeImages();
}
</script>
``
<template>
    <div class="w-full flex justify-center py-3">
        <button
            class="bg-white hover:bg-gray-100 text-gray-800 font-semibold py-2 px-4 border border-gray-400 rounded shadow"
            @click="onClick"
        >
            Merge Images
        </button>
    </div>
</template>

<style scoped></style>
