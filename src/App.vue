<script setup>
import Grid from "./components/Grid.vue";
import Image from "./components/Image.vue";


let placeholder = "https://placehold.co/500x500";
const ROWS = 3;
const COLS = 3;

let images = [];

for (let i = 0; i < ROWS; i++) {
    images[i] = [];
    for (let j = 0; j < COLS; j++) {
        images[i][j] = placeholder;
    }
}

</script>

<template>
    <div class="w-full h-screen bg-white dark:bg-slate-800">
        <div class="container mx-auto px-40">
            <p class="text-7xl text-center text-white mb-12">3x3</p>

            <Grid>

                <Image :placeholder="placeholder" />
                <Image :placeholder="placeholder" />
                <Image :placeholder="placeholder" />

                <Image :placeholder="placeholder" />
                <Image :placeholder="placeholder" />
                <Image :placeholder="placeholder" />

                <Image :placeholder="placeholder" />
                <Image :placeholder="placeholder" />
                <Image :placeholder="placeholder" />
            </Grid>

            <Toolbar />
        </div>
    </div>
</template>

<style scoped></style>
