<script setup>
import { ref } from 'vue'

const activeLink = ref('') 

const navLinks = [
  { id: 'about', label: 'About' },
  { id: 'skills', label: 'Skills' },
  { id: 'experience', label: 'Experience' },
  { id: 'projects', label: 'Projects' },
]

const setActive = (id) => {
  activeLink.value = id
}

// Reactive data
const isMobileMenuOpen = ref(false)

// Methods
const toggleMobileMenu = () => {
  isMobileMenuOpen.value = !isMobileMenuOpen.value
}

const closeMobileMenu = () => {
  isMobileMenuOpen.value = false
}

onMounted(() => {
  watch(() => useRoute().path, () => {
    isMobileMenuOpen.value = false
  })
})
</script>


<template>
  <div class="w-full">
    <div class="fixed top-0 left-0 right-0 z-50 mx-auto px-[4%] md:px-[3%] xl:px-[0%] py-6">
      <nav
        class="max-w-7xl mx-auto bg-white/15 backdrop-blur-md bg-clip-padding backdrop-filter bg-opacity-40 shadow-lg border border-gray-50/30 rounded-2xl">
        <div class="px-4 sm:px-6 lg:px-8">
          <div class="flex items-center justify-between h-14 lg:h-16">

            <!-- Logo Section -->
            <div class="flex-shrink-0">
              <a href="#" class="flex items-center" @click="setActive(), closeMobileMenu()">
                <img class="h-7 w-auto lg:h-8 transition-all duration-200 hover:scale-105" src="/images/portfolio-logo.png"
                  alt="Portfolio Logo" />
              </a>
            </div>

            <!-- Navigation Links (Desktop) -->
            <div class="hidden lg:block">
              <div class="flex items-center space-x-1 xl:space-x-2">
                <a v-for="link in navLinks" :key="link.id" :href="`#${link.id}`" @click="setActive(link.id)" :class="[
                  'text-gray-200 hover:text-[#ca8a04] px-4 py-2 rounded-lg text-base font-medium transition-all duration-200 hover:scale-105',
                  activeLink === link.id ? 'text-yellow-500 font-medium underline underline-offset-4 decoration-2' : ''
                ]">
                  {{ link.label }}
                </a>
              </div>
            </div>

            <!-- Mobile menu button -->
            <div class="lg:hidden">
              <button @click="toggleMobileMenu"
                class="inline-flex items-center justify-center p-2 rounded-lg text-gray-200 hover:text-gray-300 hover:bg-gray-100 focus:outline-none focus:ring-2 focus:ring-[#395886] transition-colors duration-200"
                :class="{ 'bg-transparent': isMobileMenuOpen }">
                <svg class="h-6 w-6 transition-transform duration-200" :class="{ 'rotate-180': isMobileMenuOpen }"
                  fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path v-if="!isMobileMenuOpen" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                    d="M4 6h16M4 12h16M4 18h16" />
                  <path v-else stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                    d="M6 18L18 6M6 6l12 12" />
                </svg>
              </button>
            </div>
          </div>
        </div>

        <!-- Mobile menu -->
        <div v-show="isMobileMenuOpen" class="lg:hidden bg-transparent border-t border-gray-500 shadow-lg rounded-b-2xl"
          :class="{ 'animate-fade-in': isMobileMenuOpen }">
          <div class="px-4 sm:px-6">
            <div class="py-4 space-y-2">

              <!-- Mobile Navigation Links -->
              <a v-for="link in navLinks" :key="link.id" :href="`#${link.id}`"
                @click="setActive(link.id), closeMobileMenu()" :class="[
                  'text-gray-200 hover:text-[#ca8a04] hover:bg-gray-300 block px-4 py-3 rounded-lg text-base font-medium transition-all duration-200',
                  activeLink === link.id ? 'text-yellow-500 font-medium bg-blue-50' : ''
                ]">
                {{ link.label }}
              </a>
            </div>
          </div>
        </div>
      </nav>
    </div>

    <!-- Spacer to prevent content from hiding behind fixed navbar -->
    <div class="h-20 lg:h-24"></div>
  </div>
</template>

<style scoped>
.poppins-text {
  font-family: 'Poppins', sans-serif;
}

@keyframes fade-in {
  from {
    opacity: 0;
    transform: translateY(-10px);
  }

  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.animate-fade-in {
  animation: fade-in 0.2s ease-out;
}
</style>
