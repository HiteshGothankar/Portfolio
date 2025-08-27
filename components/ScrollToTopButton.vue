<template>
    <div v-if="showButton" class="fixed bottom-7 right-4 md:bottom-10 md:right-5 z-50">
        <button @click="scrollToTop"
            class="bg-white/30 text-white font-bold w-9 h-9 md:w-10 md:h-10  rounded-full flex items-center justify-center shadow-md transition cursor-pointer">
            <span>🡱</span>
        </button>
    </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const showButton = ref(false)

function scrollToTop() {
    window.scrollTo({ top: 0, behavior: 'smooth' })
}

function checkScroll() {
    showButton.value = window.scrollY > 200
}

onMounted(() => {
    window.addEventListener('scroll', checkScroll)
})

onUnmounted(() => {
    window.removeEventListener('scroll', checkScroll)
})
</script>

