<template>
    <div class="lokasimu-wrapper bg-black h-screen text-center py-12 px-6">
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
        <div class="ip-address-wrapper mt-36">
            <p class="font-light">Your Public IP Address : {{ public_ip }}</p>
        </div>
        <div
            class="
                geolocation-wrapper
                bg-gray-200
                w-fit
                m-auto
                py-3
                px-12
                mt-3
                rounded-2xl
            "
        >
            <p
                class="text-4xl sm:text-7xl font-bold text-gray-900 mt-5"
                v-if="geolocation.length > 0"
            >
                <!-- {{ public_ip }} -->
                {{ geolocation[0].city }}, {{ geolocation[0].countryCode }}
            </p>
            <p class="mt-3 mb-3 text-blue-500 text-lg font-medium">
                Your IP Location
            </p>
        </div>
    </div>
</template>

<script lang="ts">
import { defineComponent, reactive, toRefs } from "vue";
import axios from "axios";
import Geolocation from "../types/Geolocation";

export default defineComponent({
    name: "YourLocation",
    setup() {
        const data = reactive({
            public_ip: "" as string,
            geolocation: <Geolocation[]>[],
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
                .then((res) => {
                    this.public_ip = res.data.ip;
                    this.getIPLocation(this.public_ip);
                })
                .catch((err) => err);
        },
        async getIPLocation(ip: string) {
            axios
                .get(`http://ip-api.com/json/${ip}`)
                .then((res) => {
                    this.geolocation = <Geolocation[]>[res.data];
                })
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
