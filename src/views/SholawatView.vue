<script setup lang="ts">
import { RouterLink } from 'vue-router'
import { ref } from 'vue'
import imgSholawatBanner from "@/assets/img/sholawat-banner.jpg"
import listSholawatJson from "@/assets/data/sholawat.json"
const listSholawat = ref(
    listSholawatJson.map(item => ({
        ...item,
        image: new URL(`/src/assets/img/${item.imgName}`, import.meta.url).href
    }))
)
</script>
<template>
    <div id="sholawat">
        <div id="greeting-wrapper">
            <img :src="imgSholawatBanner" alt="sholawat banner" class="banner-img glass" />
            <h3 class="banner-text glass">Aku berserah, karena Engkau sebaik-baik tempat bergantung.</h3>
        </div>
        <div v-for="sholawat in listSholawat" :key="sholawat.id" class="sholawat-wrapper">
            <div>
                <img :src="sholawat.image" :alt="sholawat.name" class="card-img glass" />
            </div>
            <div class="card-text-list">
                <h3 class="card-text">{{ sholawat.name }}</h3>
                <RouterLink :to="`/sholawat/${sholawat.id}`" class="btn-link">
                    <!-- https://feathericons.dev/?search=chevrons-right&iconset=feather -->
                    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="24" height="24"
                        class="main-grid-item-icon" fill="none" stroke="currentColor" stroke-linecap="round"
                        stroke-linejoin="round" stroke-width="2">
                        <polyline points="13 17 18 12 13 7" />
                        <polyline points="6 17 11 12 6 7" />
                    </svg>
                </RouterLink>
            </div>
        </div>
    </div>
</template>
<style scoped>
#sholawat {
    min-height: 100vh;
}

#greeting-wrapper {
    display: flex;
    flex-direction: column;
    align-items: center;
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

.banner-text {
    position: absolute;
    bottom: 20px;
    font-size: 1.2rem;
    text-align: center;
    padding: 0 20px;
    color: var(--vt-c-black);
    width: 90%;
    border-radius: 16px;
    font-family: "Lato", sans-serif !important;
    font-weight: 600;
    font-size: 1.2rem;
    font-style: bold;
}

.sholawat-wrapper {
    background-color: var(--vt-c-white);
    padding: 10px;
    margin-top: 10px;
    border-radius: 16px;
    display: flex;
    flex-direction: column;
}

.card-img {
    width: 100%;
    height: 220px;
    object-fit: cover;
    object-position: center;
    border-radius: 8px;
}

.card-text-list {
    padding: 10px;
    background-color: rgba(0, 166, 81, 0.2);
    border-radius: 8px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex: row;
}

.card-text {
    font-family: "Lato", sans-serif !important;
    font-weight: 600;
    font-size: 1.2rem;
    font-style: bold;
    color: var(--vt-c-black);
}

.btn-link {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 40px;
    height: 40px;
    border-radius: 50%;
    background-color: var(--app-green-5);
    color: var(--vt-c-white);
    text-decoration: none;
}
</style>