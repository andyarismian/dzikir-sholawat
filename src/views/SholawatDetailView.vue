<script setup lang="ts">
import { ref, onMounted } from 'vue'
import { useRoute, RouterLink } from 'vue-router'
const route = useRoute()
import listSholawatJson from "@/assets/data/sholawat.json"
const sholawatData = ref(null)
const imgSholawatBanner = ref('')
const sholawatName = ref('')

onMounted(async () => {
    const id = Number(route.params.id)

    const sholawat = listSholawatJson.find(s => s.id === id)

    if (sholawat) {
        sholawatName.value = sholawat.name
        const data = await import(`@/assets/data/${sholawat.json}.json`)
        sholawatData.value = data.default
        imgSholawatBanner.value = new URL(
            `/src/assets/img/${sholawat.imgName}`,
            import.meta.url
        ).href
    }
})
</script>
<template>
    <div id="sholawat-detail">
        <div id="greeting-wrapper">
            <img :src="imgSholawatBanner" alt="sholawat banner" class="banner-img glass" />
            <div class="banner-title">
                <RouterLink :to="'/sholawat'" class="btn-link glass">
                    <!-- https://feathericons.dev/?search=chevrons-left&iconset=feather -->
                    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="24" height="24"
                        class="main-grid-item-icon" fill="none" stroke="currentColor" stroke-linecap="round"
                        stroke-linejoin="round" stroke-width="2">
                        <polyline points="11 17 6 12 11 7" />
                        <polyline points="18 17 13 12 18 7" />
                    </svg>
                </RouterLink>
                <h3 class="banner-text glass" style="font-weight: 600;">{{ sholawatName }}</h3>
            </div>
        </div>
        <div v-if="sholawatData">
            <div v-for="item in sholawatData" :key="item.id" id="sholawat-item">
                <div class="sholawat-card">
                    <p style="font-size: 1.2em; font-weight: bold; text-align: right;margin-bottom:8px;">{{ item.arab
                    }}</p>
                    <p style="margin-bottom:8px;">{{ item.latin }}</p>
                </div>
                <div class="sholawat-sub-card">
                    <p style="font-weight: lighter; font-style: italic;">"{{ item.id }}"</p>
                </div>
            </div>
        </div>
        <div v-else>Loading...</div>
    </div>
</template>
<style scoped>
#sholawat-item {
    background-color: var(--vt-c-white);
    padding: 10px;
    margin-top: 10px;
    border-radius: 16px;
}

.sholawat-card {
    background-color: var(--app-green-3);
    border-radius: 8px;
    padding: 10px;
    margin-top: 10px;
    color: var(--vt-c-white)
}

#sholawat-detail {
    min-height: 100vh;
}

#greeting-wrapper {
    display: flex;
    flex-direction: column;
    align-items: center;
    color: var(--vt-c-white);
    font-family: "Lato", sans-serif !important;
    font-weight: 300;
    font-size: 1.2rem;
    font-style: bold;
    height: 230px;
    width: 100%;
    border-radius: 16px;
    position: relative;
}

.banner-img {
    width: 100%;
    height: 100%;
    image-rendering: pixelated;
    object-fit: cover;
    border-radius: 16px;
}

.banner-title {
    position: absolute;
    bottom: 20px;
    width: 90%;
    display: flex;
    justify-content: center;
    flex-direction: row;
    align-items: center;
    gap: 10px;
}

.banner-text {
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 1.2rem;
    text-align: center;
    padding: 0 20px;
    color: var(--vt-c-black);
    width: 80%;
    border-radius: 16px;
    min-height: 50px;
}

.btn-link {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 50px !important;
    height: 50px !important;
    border-radius: 50%;
    background-color: var(--app-green-5);
    color: var(--vt-c-white);
    text-decoration: none;
    opacity: 0.8;
}
</style>