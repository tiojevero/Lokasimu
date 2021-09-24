<template>
    <div class="lokasimu-wrapper bg-black h-screen text-center py-12">
        <h1
            class="
                text-8xl
                font-medium
                bg-clip-text
                text-transparent
                bg-gradient-to-r
                from-pink-400
                to-blue-500
                w-fit
                m-auto
            "
        >
            lokasimu.
        </h1>
        <p class="mt-4">Your IP is : {{ public_ip }}</p>
    </div>
</template>

<script setup lang="ts">
import { ref } from "vue";

const public_ip = ref("1.2.3.4");
</script>

<style lang="scss" scoped>
@import url("https://fonts.googleapis.com/css2?family=Inter:wght@100;200;300;400;500;600;700;800;900&family=Yellowtail&display=swap");
* {
    color: #eee;
    font-family: Inter, sans-serif;
}

.w-fit {
    width: fit-content;
}

.lokasimu-wrapper {
    h1 {
        font-family: YellowTail, sans-serif;
    }
}
</style>
