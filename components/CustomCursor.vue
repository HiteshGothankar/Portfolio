<template>
  <div ref="cursor" class="custom-cursor hidden sm:hidden md:hidden lg:block" />
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { gsap } from 'gsap'

const cursor = ref(null)

onMounted(() => {
  const moveCursor = (e) => {
    gsap.to(cursor.value, {
      x: e.clientX,
      y: e.clientY,
      duration: 0.8,
      ease: 'power2.out',
    })
  }

  window.addEventListener('mousemove', moveCursor)

  // Clean up
  onUnmounted(() => {
    window.removeEventListener('mousemove', moveCursor)
  })
})
</script>

<style scoped>
.custom-cursor {
  position: fixed;
  top: 0;
  left: 0;
  width: 20px;
  height: 20px;
  pointer-events: none;
  background-color: rgb(175, 185, 196);
  border-radius: 50%;
  transform: translate(-50%, -50%);
  z-index: 999;
  opacity: 0.6;
}
</style>
