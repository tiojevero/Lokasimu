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
        <h5 class="font-light text-xl text-gray-200">
            Your IP Address Geolocator
        </h5>
        <p class="mt-36 mb-3 font-light text-lg">Your Public IP Address</p>
        <div
            class="
                ip-address-wrapper
                bg-gray-100
                w-fit
                m-auto
                py-4
                px-8
                rounded-2xl
            "
        >
            <span class="text-7xl font-bold text-gray-900">{{
                public_ip
            }}</span>
        </div>
    </div>
</template>

<script lang="ts">
import { defineComponent, reactive, toRefs } from "vue";
import axios from "axios";

export default defineComponent({
    name: "YourLocation",
    setup() {
        const data = reactive({
            public_ip: "" as string,
        });

        return { ...toRefs(data) };
    },
    mounted() {
        this.getIPAddress();
    },
    methods: {
        async getIPAddress() {
            axios
                .get("https://api.ipify.org?format=json")
                .then((res) => (this.public_ip = res.data.ip))
                .catch((err) => err);
        },
    },
});
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
