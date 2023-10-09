<script setup>
import { ref } from 'vue'

const props = defineProps(["placeholder"]);
const emit = defineEmits(["update:placeholder"]);

const placeholder = ref(props.placeholder);

function onClick() {
    placeholder.value = "https://placehold.co/500x500";

    let input = document.createElement('input')
    input.type = 'file'
    input.accept = 'image/*'

    input.onchange = e => {
        let file = e.target.files[0]
        let reader = new FileReader()
        reader.readAsDataURL(file)
        reader.onload = e => {
            placeholder.value = e.target.result
            emit("update:placeholder", e.target.result)
        }
    }

    input.click()
}
</script>

<template>
    <div class="image">
        <img :src="placeholder" class="w-full aspect-square" />
        <div class="overlay" @click="onClick">
            <div class="text">🖼️</div>
        </div>
    </div>
</template>

<style scoped>
.image {
    position: relative;
    width: 100%;
    height: 100%;
}

.image img {
    width: 100%;
    height: 100%;
    object-fit: cover;
}

.image .overlay {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    display: grid;
    place-items: center;
    background-color: rgba(0, 0, 0, 0.5);
    opacity: 0;
    transition: opacity 0.2s ease-in-out;

    cursor: pointer;
}

.image:hover .overlay {
    opacity: 1;
}

.image .overlay .text {
    font-size: 5rem;
    color: white;
}

.image input {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
}
</style>
