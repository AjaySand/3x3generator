<script setup>
import { ref } from "vue";
import Grid from "./components/Grid.vue";
import ImageItem from "./components/ImageItem.vue";
import Toolbar from "./components/Toolbar.vue";

let placeholder = "https://placehold.co/500x500";
const ROWS = 3;
const COLS = 3;

let images = [];
let mergedImage = ref("");
let numImagesMerged = ref(0);

for (let i = 0; i < ROWS; i++) {
    images[i] = [];
    for (let j = 0; j < COLS; j++) {
        images[i][j] = placeholder;
    }
}

function mergeImages() {
    let canvas = document.createElement("canvas");
    let ctx = canvas.getContext("2d");

    canvas.width = 1500;
    canvas.height = 1500;

    for (let i = 0; i < ROWS; i++) {
        for (let j = 0; j < COLS; j++) {
            let image = new Image();
            image.src = images[i][j];
            image.style = "width: 100%; height: 100%; object-fit: cover;";

            image.onload = () => {
                ctx.drawImage(image, i * 500, j * 500, 500, 500);
                numImagesMerged.value++;

                if (numImagesMerged.value == ROWS * COLS) {
                    mergedImage.value = canvas.toDataURL("image/png");
                }
            };
        }
    }

    if (numImagesMerged.value == ROWS * COLS) {
        mergedImage.value = canvas.toDataURL("image/png");
    }
}
</script>

<template>
    <div class="w-full bg-white dark:bg-slate-800">
        <div class="container mx-auto 2xl:px-96 xl:px-80 md:px-40">
            <p class="text-7xl text-center text-white mb-12">3x3</p>

            <Grid>
                <template v-for="(row, i) in images" :key="i">
                    <ImageItem
                        v-for="(image, j) in row"
                        :key="j"
                        :placeholder="image"
                        @update:placeholder="(value) => (images[i][j] = value)"
                    />
                </template>
            </Grid>

            <Toolbar :mergeImages="mergeImages" />

            <img :src="mergedImage" v-if="mergedImage != ''" />
        </div>
    </div>
</template>

<style scoped></style>
