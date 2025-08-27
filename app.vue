<script setup>

useHead({
  title: 'Hitesh Gothankar | Portfolio',
  meta: [
    { name: 'Hitesh Gothankar | Portfolio', content: `Hitesh's Portfolio website` }
  ],
  link: [
    {
      rel: 'stylesheet',
      href: 'https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap', //Poppins font
    },
  ],
})

import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'
import { onMounted } from 'vue'

// gsap code
gsap.registerPlugin(ScrollTrigger)

// refs for gsap animations
const skills = ref(null)
const about = ref(null)
const myname = ref(null)

// Code for experience section
let observer

onMounted(() => {
  observer = new IntersectionObserver((entries) => {
    entries.forEach((entry) => {
      const el = entry.target
      if (entry.isIntersecting) {
        el.classList.add('show-animation')
        observer.unobserve(el) // Animate once and stop watching
      }
    })
  }, {
    threshold: 0.1
  })

  const elements = document.querySelectorAll('.tlcontainer')
  elements.forEach((el) => observer.observe(el))

  // name gsap code
  gsap.from(myname.value, {
    x: -10,
    opacity: 0,
    duration: 1,
    ease: 'linear',
    delay: 0.8,
  })

  // skills section gsap code
  const tl = gsap.timeline({
    scrollTrigger: {
      trigger: skills.value,
      start: 'top 50%',
      delay: 1,
      // markers: true,
    }
  })

  tl.from('.skills_content', {
    y: 15,
    opacity: 0,
    duration: 2,
    ease: 'ease',
    // delay: 0.1,
    stagger: 0.2,
  })


  // about section gsap code
  const tle = gsap.timeline({
    scrollTrigger: {
      trigger: about.value,
      start: 'top 50%',
      // markers: true,
    }
  })

  tle.from('.about-image', {
    x: 15,
    opacity: 0,
    duration: 1,
    // start:'top 70%',
    ease: 'in'
  })
    .from('.about-text', {
      x: 15,
      opacity: 0,
      duration: 0.8,
      ease: 'in'
    }, "-=0.3")
    .from('.about-button', {
      x: 15,
      opacity: 0,
      duration: 0.8,
      ease: 'in'
    }, "-=0.3")

})

// clean up
onBeforeUnmount(() => {
  const elements = document.querySelectorAll('.tlcontainer')
  elements.forEach(el => observer?.unobserve(el))
  observer?.disconnect()
})

</script>

<template>
  <div class="relative w-full min-h-screen">
    <div class="relative z-10 bg-gradient-to-r from-[#041b35] via-[#042951] to-[#041b35]/95 min-h-screen px-3 md:px-2">

      <Squares :speed="0.2" :square-size="40" direction="up" border-color="#181818" z-index="-z-100" />
      <CustomCursor />

      <Navbar />

      <!-- Hero Section -->
      <section id="home">
        <div class="min-h-screen overflow-hidden pb-17 lg:pb-0">
          <!-- Main Content -->
          <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="grid grid-cols-1 lg:grid-cols-2 gap-0 lg:gap-12 items-center justify-center min-h-[80vh]">

              <!-- left content -->
              <div class="text-left order-2 lg:order-1">

                <div class="space-y-0 md:space-y-2">
                  <div
                    class="mt-4 md:mt-0 w-fit text-xs md:text-sm xl:text-[14px] 2xl:text-[16px] px-1 md:px-2 py-1 md:py-1 font-semibold tracking-wide text-white border-1 border-gray-700 bg-transparent rounded-2xl ">
                    <span class="animate-pulse duration-500">👋</span> Hey there!&nbsp;
                  </div>
                  <div class="text-gray-300 font-bold text-2xl md:text-4xl 2xl:text-5xl mt-4">I'm</div>
                  <div ref="myname"
                    class="text-[28px] md:text-5xl xl:text-6xl font-bold disabled={false} speed={3} shiny-name">
                    Hitesh Gothankar
                  </div>

                  <h3 class="text-xl md:text-3xl 2xl:4xl font-normal text-white mb-5 md:mb-8">
                    Frontend Developer
                  </h3>

                  <p class="mb-6 md:mb-7 mx-auto text-white text-sm md:text-lg xl:text-lg 2xl:xl: font-normal">
                    Driven by a passion for clean code and compelling design, creating responsive and engaging user
                    interfaces that adapt beautifully across devices with precision and creativity.
                  </p>
                </div>

                <div>
                  <div
                    class="hidden lg:block hover:shadow-[0_0_20px_5px_rgba(59,130,246,0.4)] w-fit text-sm md:text-lg px-4 md:px-4 py-2 hover:bg-gray-300 hover:text-[#042951] font-medium rounded-lg text-gray-200 backdrop-blur-2xl outline-1 outline-gray-300 transition-all duration-300">
                    <a href="mailto:gothankarhitesh05@gmail.com">Contact Me</a>
                  </div>
                  <div
                    class="lg:hidden shadow-[0_0_20px_5px_rgba(59,130,246,0.4)] w-fit text-sm md:text-lg px-4 md:px-4 py-2 bg-gray-300 text-[#042951] font-medium rounded-lg backdrop-blur-2xl outline-1 outline-gray-300 ">
                    <a href="mailto:gothankarhitesh05@gmail.com">Contact Me</a>
                  </div>
                </div>

              </div>

              <!-- right content -->
              <div class="h-65 md:h-95 lg:h-auto mx-auto order-1 lg:order-2 overflow-hidden">
                <img src="/public/images/heroimg.webp"
                  class="w-full h-full object-cover drop-shadow-xs drop-shadow-black" alt="">
              </div>

            </div>

            <!-- animate scroll dot -->
            <div class="hidden lg:flex justify-center items-center relative lg:bottom-9 xl:bottom-7 cursor-pointer">
              <div class="h-[60px] w-[30px] border-3 border-white rounded-3xl flex justify-center bg-white/10 p-2">
                <div class="h-[12px] w-[12px] rounded-full bg-white animate-scroll-dot"></div>
              </div>
            </div>
          </div>
        </div>
      </section>

      <!-- About Section -->
      <span id="about" class="mt-[-100px] pb-[100px] block">&nbsp;</span>
      <section class="about">
        <div class="overflow-hidden pb-17 lg:pb-30">
          <div class="max-w-7xl h-auto mx-auto px-4 sm:px-6 lg:px-8">
            <h1
              class="text-white text-4xl md:text-5xl xl:text-6xl font-medium mb-10 border-l-7 pl-3 md:pl-5 border-[#ca8a04]">
              ABOUT ME</h1>
            <div ref="about" class="flex flex-col lg:flex-row gap-8 lg:gap-15 items-center justify-center">

              <!-- Outer gradient border wrapper -->
              <div
                class="about-image shadow-[0_0_20px_5px_rgba(59,130,246,0.4)] relative size-55 md:size-68 lg:size-80 xl:size-80 mx-auto rounded-full bg-gradient-to-r from-blue-500 via-sky-200 to-blue-500 p-[3px]">
                <div
                  class="rounded-full w-full h-full bg-white/10 backdrop-blur-md bg-clip-padding border border-white/10 overflow-hidden shadow-inner">
                  <img src="./public/images/MyPic.png"
                    class="w-full h-full object-cover object-top drop-shadow-2xl drop-shadow-sky-100" />
                </div>
              </div>

              <div class="w-full lg:w-[60%] xl:w-[65%]">

                <div class="about-text space-y-1 xl:space-y-2">
                  <p class="text-gray-300 font-normal text-sm md:text-lg lg:text-[16px] xl:text-lg mb-3 xl:mb-4">
                    Hi, I'm Hitesh Gothankar, a passionate Frontend Developer with hands-on experience in building
                    dynamic and responsive web applications. I specialize in modern JavaScript frameworks like React.js,
                    Vue.js, and Nuxt.js.
                  </p>

                  <p class="text-gray-300 font-normal text-sm md:text-lg lg:text-[16px] xl:text-lg mb-5 xl:mb-7">
                    I enjoy working on interactive UI designs and animations, often leveraging GSAP to bring interfaces
                    to life. Staying current with evolving frontend technologies is a key part of my workflow. I’m always
                    eager to take on new challenges that push the boundaries of creativity and code.
                  </p>
                </div>

                <div class="about-button">
                  <div
                    class="hidden lg:block hover:shadow-[0_0_20px_5px_rgba(59,130,246,0.4)] w-fit text-sm md:text-lg px-5 md:px-5 py-2 hover:bg-gray-300 hover:text-[#042951] font-normal rounded-lg text-gray-200 backdrop-blur-2xl outline-1 outline-gray-300 transition-all duration-300">
                    <a href="mailto:gothankarhitesh05@gmail.com">Contact Me</a>
                    <!-- <a href="/resume.pdf" target="_blank">Resume</a> -->
                  </div>
                  <div
                    class="lg:hidden shadow-[0_0_20px_5px_rgba(59,130,246,0.4)] w-fit text-sm md:text-lg px-5 md:px-5 py-2 bg-gray-300 text-[#042951] font-normal rounded-lg backdrop-blur-2xl outline-1 outline-gray-300 ">
                    <a href="mailto:gothankarhitesh05@gmail.com">Contact Me</a>
                    <!-- <a href="/resume.pdf" target="_blank">Resume</a> -->
                  </div>
                </div>

              </div>

            </div>
          </div>
        </div>
      </section>


      <!-- Skills & Technologies -->
      <span id="skills" class="mt-[-100px] pb-[100px] block">&nbsp;</span>
      <section class="techstack">
        <div class="overflow-hidden pb-17 lg:pb-30">
          <div class="mx-auto px-4 sm:px-6 lg:px-8">
            <div
              class="max-w-2xl lg:max-w-3xl xl:max-w-4xl h-auto mx-auto px-4 sm:px-6 lg:px-8 py-10 border border-gray-500 rounded-2xl bg-black/15 backdrop-filter bg-opacity-40 backdrop-blur-2xl shadow-[0_0_20px_5px_rgba(59,130,246,0.08)]">
              <h1 class="text-white text-3xl md:text-4xl lg:text-[40px] xl:text-5xl font-normal mb-10 text-center">
                SKILLS &
                TECHNOLOGIES
              </h1>
              <div ref="skills"
                class="grid grid-cols-2 md:grid-cols-5 lg:grid-cols-5 justify-center items-center mx-4 md:mx-8 lg:mx-12 xl:mx-14 gap-6">
                <!-- HTML -->
                <div class="skills_content relative group flex justify-center">
                  <div
                    class="bg-transparent bg-clip-padding backdrop-filter bg-opacity-40 backdrop-blur-md size-20 lg:size-22 xl:size-25 p-4 rounded-lg border-2 border-[#fc490b] shadow-[0_0_15px_3px_rgba(252,73,11,0.25)]">
                    <img src="./public/images/icons/html-5.png" alt="">
                    <div
                      class="absolute left-1/2 -translate-x-1/2 bottom-full mb-2 px-3 py-1 rounded outline outline-gray-700 bg-black text-white text-sm opacity-0 group-hover:opacity-100 transition-opacity duration-200 whitespace-nowrap z-10">
                      HTML
                    </div>
                  </div>
                </div>

                <!-- CSS -->
                <div class="skills_content relative group flex justify-center">
                  <div
                    class="bg-transparent bg-clip-padding backdrop-filter bg-opacity-40 backdrop-blur-md size-20 lg:size-22 xl:size-25 p-4 rounded-lg border-2 border-[#2196f3] shadow-[0_0_15px_3px_rgba(33,150,243,0.25)]">
                    <img src="./public/images/icons/css-3.png" alt="">
                    <div
                      class="absolute left-1/2 -translate-x-1/2 bottom-full mb-2 px-3 py-1 rounded outline outline-gray-700 bg-black text-white text-sm opacity-0 group-hover:opacity-100 transition-opacity duration-200 whitespace-nowrap z-10">
                      CSS
                    </div>
                  </div>
                </div>


                <!-- JavaScript -->
                <div class="skills_content relative group flex justify-center">
                  <div
                    class="bg-transparent bg-clip-padding backdrop-filter bg-opacity-40 backdrop-blur-md size-20 lg:size-22 xl:size-25 p-4 rounded-lg border-2 border-[#f1db4f] shadow-[0_0_15px_3px_rgba(241,219,79,0.25)]">
                    <img src="./public/images/icons/js.png" alt="">
                    <div
                      class="absolute left-1/2 -translate-x-1/2 bottom-full mb-2 px-3 py-1 rounded outline outline-gray-700 bg-black text-white text-sm opacity-0 group-hover:opacity-100 transition-opacity duration-200 whitespace-nowrap z-10">
                      JavaScript
                    </div>
                  </div>
                </div>

                <!-- Tailwind CSS -->
                <div class="skills_content relative group flex justify-center">
                  <div
                    class="bg-transparent bg-clip-padding backdrop-filter bg-opacity-40 backdrop-blur-md size-20 lg:size-22 xl:size-25 p-4 rounded-lg border-2 border-[#38bdf8] shadow-[0_0_15px_3px_rgba(56,189,248,0.25)]">
                    <img src="./public/images/icons/Tailwind CSS.png" alt="">
                    <div
                      class="absolute left-1/2 -translate-x-1/2 bottom-full mb-2 px-3 py-1 rounded outline outline-gray-700 bg-black text-white text-sm opacity-0 group-hover:opacity-100 transition-opacity duration-200 whitespace-nowrap z-10">
                      Tailwind CSS
                    </div>
                  </div>
                </div>

                <!-- React JS -->
                <div class="skills_content relative group flex justify-center">
                  <div
                    class="bg-transparent bg-clip-padding backdrop-filter bg-opacity-40 backdrop-blur-md size-20 lg:size-22 xl:size-25 p-4 rounded-lg border-2 border-[#60dafb] shadow-[0_0_15px_3px_rgba(96,218,251,0.25)]">
                    <img src="./public/images/icons/React.png" alt="">
                    <div
                      class="absolute left-1/2 -translate-x-1/2 bottom-full mb-2 px-3 py-1 rounded outline outline-gray-700 bg-black text-white text-sm opacity-0 group-hover:opacity-100 transition-opacity duration-200 whitespace-nowrap z-10">
                      React JS
                    </div>
                  </div>
                </div>

                <!-- Node JS -->
                <div class="skills_content relative group flex justify-center">
                  <div
                    class="bg-transparent bg-clip-padding backdrop-filter bg-opacity-40 backdrop-blur-md size-20 lg:size-22 xl:size-25 p-4 rounded-lg border-2 border-[#83cd2a] shadow-[0_0_15px_3px_rgba(131,205,42,0.25)]">
                    <img src="./public/images/icons/Node.js.png" alt="">
                    <div
                      class="absolute left-1/2 -translate-x-1/2 bottom-full mb-2 px-3 py-1 rounded outline outline-gray-700 bg-black text-white text-sm opacity-0 group-hover:opacity-100 transition-opacity duration-200 whitespace-nowrap z-10">
                      Node JS
                    </div>
                  </div>
                </div>

                <!-- Vue JS -->
                <div class="skills_content relative group flex justify-center">
                  <div
                    class="bg-transparent bg-clip-padding backdrop-filter bg-opacity-40 backdrop-blur-md size-20 lg:size-22 xl:size-25 p-4 rounded-lg border-2 border-[#41b883] shadow-[0_0_15px_3px_rgba(65,184,131,0.25)]">
                    <img src="./public/images/icons/Vue.js.png" alt="">
                    <div
                      class="absolute left-1/2 -translate-x-1/2 bottom-full mb-2 px-3 py-1 rounded outline outline-gray-700 bg-black text-white text-sm opacity-0 group-hover:opacity-100 transition-opacity duration-200 whitespace-nowrap z-10">
                      Vue JS
                    </div>
                  </div>
                </div>

                <!-- Nuxt JS -->
                <div class="skills_content relative group flex justify-center">
                  <div
                    class="bg-transparent bg-clip-padding backdrop-filter bg-opacity-40 backdrop-blur-md size-20 lg:size-22 xl:size-25 p-4 rounded-lg border-2 border-[#02dc82] shadow-[0_0_15px_3px_rgba(2,220,130,0.25)]">
                    <img src="./public/images/icons/nuxt.svg" alt="">
                    <div
                      class="absolute left-1/2 -translate-x-1/2 bottom-full mb-2 px-3 py-1 rounded outline outline-gray-700 bg-black text-white text-sm opacity-0 group-hover:opacity-100 transition-opacity duration-200 whitespace-nowrap z-10">
                      Nuxt JS
                    </div>
                  </div>
                </div>

                <!-- GitHub -->
                <div class="skills_content relative group flex justify-center">
                  <div
                    class="bg-transparent bg-clip-padding backdrop-filter bg-opacity-40 backdrop-blur-md size-20 lg:size-22 xl:size-25 p-4 rounded-lg border-2 border-[#5C6BC0] shadow-[0_0_15px_3px_rgba(92,107,192,0.25)]">
                    <img src="./public/images/icons/github.png" alt="">
                    <div
                      class="absolute left-1/2 -translate-x-1/2 bottom-full mb-2 px-3 py-1 rounded outline outline-gray-700 bg-black text-white text-sm opacity-0 group-hover:opacity-100 transition-opacity duration-200 whitespace-nowrap z-10">
                      GitHub
                    </div>
                  </div>
                </div>

                <!-- GSAP -->
                <div class="skills_content relative group flex justify-center">
                  <div
                    class="bg-transparent bg-clip-padding backdrop-filter bg-opacity-40 backdrop-blur-md size-20 lg:size-22 xl:size-25 p-4 rounded-lg border-2 border-[#fffde2] shadow-[0_0_15px_3px_rgba(255,253,226,0.25)]">
                    <img src="./public/images/icons/gsap.webp" alt="">
                    <div
                      class="absolute left-1/2 -translate-x-1/2 bottom-full mb-2 px-3 py-1 rounded outline outline-gray-700 bg-black text-white text-sm opacity-0 group-hover:opacity-100 transition-opacity duration-200 whitespace-nowrap z-10">
                      GSAP
                    </div>
                  </div>
                </div>

              </div>
            </div>
          </div>
        </div>
      </section>


      <!-- Experience -->
      <span id="experience" class="mt-[-100px] pb-[100px] block">&nbsp;</span>
      <section class="experience">
        <div class="overflow-hidden pb-10 lg:pb-20">
          <div class="max-w-7xl h-auto mx-auto px-4 sm:px-6 lg:px-8">
            <h1
              class="text-white text-4xl md:text-5xl xl:text-6xl font-medium mb-10 border-l-7 pl-3 md:pl-5 border-[#ca8a04]">
              EXPERIENCE</h1>

              <div class="timeline">

              <div class="tlcontainer left-container">
                <div class="circle font-bold text-lg">
                  <div
                    class="bg-white animate-pulse duration-300 rounded-full h-[12px] w-[12px] md:h-[14px] md:w-[14px] lg:h-[18px] lg:w-[18px]">
                  </div>
                </div>
                <div class="bg-blue-300 text-box shadow-[0_0_5px_1px_rgba(59,130,246,0.1)]">
                  <h2
                    class="text-[16px] md:text-lg xl:text-[19px] text-[#042951] mb-1 border-l-5 pl-2 border-[#dba020]">
                    April 2025 - Present</h2>
                  <h1 class="text-xl md:text-[22px] xl:text-2xl font-medium text-[#042951]">Web Developer</h1>
                  <h3 class="text-[16px] md:text-lg xl:text-[18px] text-gray-800 mb-1">Bricsa Consulting Pvt. Ltd.</h3>
                  <span class="left-container-arrow"></span>
                </div>
              </div>

              <div class="tlcontainer right-container">
                <div class="circle font-bold text-lg">
                  <div class="bg-white rounded-full h-[12px] w-[12px] md:h-[14px] md:w-[14px] lg:h-[18px] lg:w-[18px]">
                  </div>
                </div>
                <div class="bg-blue-300 text-box shadow-[0_0_5px_1px_rgba(59,130,246,0.1)] ">
                  <h2
                    class="text-[16px] md:text-lg xl:text-[19px] text-[#042951] mb-1 border-l-5 pl-2 border-[#dba020]">
                    Dec 2024 - Jan 2025</h2>
                  <h1 class="text-xl md:text-[22px] xl:text-2xl font-medium text-[#042951]">Frontend Developer</h1>
                  <h3 class="text-[16px] md:text-lg xl:text-[18px] text-gray-800 mb-1">Bonum eDesign LLP</h3>
                  <span class="right-container-arrow"></span>
                </div>
              </div>

            </div>
          </div>
        </div>
      </section>


      <!-- Projects -->
      <span id="projects" class="mt-[-100px] pb-[100px] block">&nbsp;</span>
      <section class="education">
        <div class="overflow-hidden pb-15 lg:pb-30">
          <div class="max-w-7xl h-auto mx-auto px-4 sm:px-6 lg:px-8">
            <h1
              class="text-white text-4xl md:text-5xl xl:text-6xl font-medium mb-10 border-l-7 pl-3 md:pl-5 border-[#ca8a04]">
              PROJECTS
            </h1>
            <div>
              <div
                class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 justify-center items-center gap-10 lg:gap-6 xl:gap-8 xl:mx-5">

                <!-- Card 1 -->
                <div
                  class="shadow-[0_0_20px_5px_rgba(59,130,246,0.2)] w-full h-[300px] md:h-[350px] lg:h-[360px] xl:h-[365px] group relative bg-[#040f1d] rounded-xl overflow-hidden transition-all duration-500 hover:-translate-y-2">
                  <div class="relative overflow-hidden h-50 md:h-60 lg:h-65 w-full">
                    <img src="/images/TechHatch.png" alt="Techhatch"
                      class="w-full h-full object-cover transition-transform duration-700 group-hover:scale-110">
                    <div
                      class="absolute inset-0 bg-gradient-to-t from-black/60 to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-500">
                    </div>
                    <div
                      class="absolute bottom-0 left-0 right-0 p-4 translate-y-10 opacity-100 lg:opacity-0 group-hover:translate-y-0 lg:group-hover:opacity-100 transition-all duration-500">
                      <div class="flex flex-col mb-10 lg:flex-row lg:mb-0 justify-end items-end gap-3">
                        <div
                          class="cursor-pointer w-9 h-9 md:w-10 md:h-10 rounded-full bg-gradient-to-r from-white to-white text-center flex justify-center items-center p-2">
                          <a href="https://techhatch-template.vercel.app" target="_blank">
                            <img src="/images/icons/play.png" alt="">
                          </a>
                        </div>
                        <div
                          class="cursor-pointer w-9 h-9 md:w-10 md:h-10 rounded-full bg-gradient-to-r from-white to-white text-center flex justify-center items-center p-2">
                          <a href="https://github.com/HiteshGothankar/TechHatch" target="_blank">
                            <img src="/images/github.png" alt="">
                          </a>
                        </div>
                      </div>
                    </div>
                  </div>

                  <div class="p-5 w-full h-auto">
                    <div class="flex justify-between items-start">
                      <div>
                        <h3 class="text-xl md:text-2xl font-bold text-white mb-2">TechHatch<i
                            class="fa-solid fa-arrow-up-right-from-square" style="color: #395886"></i></h3>
                        <p class="text-[13px] md:text-sm font-semibold">
                          <span class="text-green-600">#NUXT&nbsp;&nbsp;</span>
                          <span class="text-sky-600">#Tailwind CSS&nbsp;&nbsp;</span>
                          <span class="text-[#fffde2]">#GSAP&nbsp;&nbsp;</span>
                        </p>
                      </div>
                    </div>
                  </div>
                </div>

                <!-- card 2 -->
                <div
                  class="shadow-[0_0_20px_5px_rgba(59,130,246,0.2)] w-full h-[300px] md:h-[350px] lg:h-[360px] xl:h-[365px] group relative bg-[#040f1d] rounded-xl overflow-hidden transition-all duration-500 hover:-translate-y-2">
                  <div class="relative overflow-hidden h-50 md:h-60 lg:h-65 w-full">
                    <img src="/images/spylt.png" alt="SPYLT"
                      class="w-full h-full object-cover object-center transition-transform duration-700 group-hover:scale-110">
                    <div
                      class="absolute inset-0 bg-gradient-to-t from-black/60 to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-500">
                    </div>
                    <div
                      class="absolute bottom-0 left-0 right-0 p-4 translate-y-10 opacity-100 lg:opacity-0 group-hover:translate-y-0 lg:group-hover:opacity-100 transition-all duration-500">
                      <div class="flex flex-col mb-10 lg:flex-row lg:mb-0 justify-end items-end gap-3">
                        <div
                          class="cursor-pointer w-9 h-9 md:w-10 md:h-10 rounded-full bg-gradient-to-r from-white to-white text-center flex justify-center items-center p-2">
                          <a href="https://animated-spylt.vercel.app" target="_blank">
                            <img src="/images/icons/play.png" alt="">
                          </a>
                        </div>
                        <div
                          class="cursor-pointer w-9 h-9 md:w-10 md:h-10 rounded-full bg-gradient-to-r from-white to-white text-center flex justify-center items-center p-2">
                          <a href="https://github.com/HiteshGothankar/SPYLT" target="_blank">
                            <img src="/images/github.png" alt="">
                          </a>
                        </div>
                      </div>
                    </div>
                  </div>

                  <div class="p-5 w-full h-auto">
                    <div class="flex justify-between items-start">
                      <div>
                        <h3 class="text-xl md:text-2xl font-bold text-white mb-2">Spylt<i
                            class="fa-solid fa-arrow-up-right-from-square" style="color: #395886"></i></h3>
                        <p class="text-[13px] md:text-sm font-semibold">
                          <span class="text-[#3aafcf]">#REACT&nbsp;&nbsp;</span>
                          <span class="text-sky-600">#Tailwind CSS&nbsp;&nbsp;</span>
                          <span class="text-[#fffde2]">#GSAP&nbsp;&nbsp;</span>
                        </p>
                      </div>
                    </div>
                  </div>
                </div>

                <!-- Card 3 -->
                <div
                  class="shadow-[0_0_20px_5px_rgba(59,130,246,0.2)] w-full h-[300px] md:h-[350px] lg:h-[360px] xl:h-[365px] group relative bg-[#040f1d] rounded-xl overflow-hidden transition-all duration-500 hover:-translate-y-2">
                  <div class="relative overflow-hidden h-50 md:h-60 lg:h-65 w-full">
                    <img src="/images/weatherapp.png" alt="Weather App"
                      class="w-full h-full object-cover object-center transition-transform duration-700 group-hover:scale-110">
                    <div
                      class="absolute inset-0 bg-gradient-to-t from-black/60 to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-500">
                    </div>
                    <div
                      class="absolute bottom-0 left-0 right-0 p-4 translate-y-10 opacity-100 lg:opacity-0 group-hover:translate-y-0 lg:group-hover:opacity-100 transition-all duration-500">
                      <div class="flex flex-col mb-10 lg:flex-row lg:mb-0 justify-end items-end gap-3">
                        <div
                          class="cursor-pointer w-9 h-9 md:w-10 md:h-10 rounded-full bg-gradient-to-r from-white to-white text-center flex justify-center items-center p-2">
                          <a href="https://see-today-weather.vercel.app" target="_blank">
                            <img src="/images/icons/play.png" alt="">
                          </a>
                        </div>
                        <div
                          class="cursor-pointer w-9 h-9 md:w-10 md:h-10 rounded-full bg-gradient-to-r from-white to-white text-center flex justify-center items-center p-2">
                          <a href="https://github.com/HiteshGothankar/Weather-App" target="_blank">
                            <img src="/images/github.png" alt="">
                          </a>
                        </div>
                      </div>
                    </div>
                  </div>

                  <div class="p-5 w-full h-auto">
                    <div class="flex justify-between items-start">
                      <div>
                        <h3 class="text-xl md:text-2xl font-bold text-white mb-2">Weather App<i
                            class="fa-solid fa-arrow-up-right-from-square" style="color: #395886"></i></h3>
                        <p class="text-[13px] md:text-sm font-semibold">
                          <span class="text-green-600">#Nuxt&nbsp;&nbsp;</span>
                          <span class="text-sky-600">#Tailwind CSS</span>
                        </p>
                      </div>
                    </div>
                  </div>
                </div>

              </div>
            </div>
          </div>
        </div>
      </section>

    </div>

    <section id="footer">
      <Footer />
    </section>

    <!-- scroll to top -->
    <ScrollToTopButton />
  </div>
</template>

<style scoped>
.poppins-text {
  font-family: 'Poppins', sans-serif;
}

/* css for name */
.shiny-name {
  color: transparent;
  background: linear-gradient(120deg,
      rgb(253, 224, 71),
      rgb(202, 138, 4),
      rgb(253, 224, 71));
  background-size: 200% 100%;
  -webkit-background-clip: text;
  background-clip: text;
  display: inline-block;
  animation: shine 5s ease-in-out infinite;
}

.shiny-name.disabled {
  animation: none;
}

/* .shiny-title {
  color: transparent;
  background: linear-gradient(120deg,
      rgb(235, 238, 240),
      rgb(255, 255, 255),
      rgb(235, 238, 240));
  background-size: 200% 100%;
  -webkit-background-clip: text;
  background-clip: text;
  display: inline-block;
  animation: shine 5s ease-in-out infinite;
}

.shiny-title.disabled {
  animation: none;
} */

@keyframes shine {
  0% {
    background-position: 100%;
  }

  100% {
    background-position: -100%;
  }
}

* {
  font-family: 'Poppins';
}


/* css for scroll dot */
.animate-scroll-dot {
  animation: scroll 2s ease-in-out infinite;
}

@keyframes scroll {

  0%,
  100% {
    transform: translateY(0px)
  }

  50% {
    transform: translateY(24px)
  }
}


/* css for experience section */
.timeline {
  position: relative;
  max-width: 980px;
  margin: 40px auto;
}

.tlcontainer {
  padding: 10px 50px;
  position: relative;
  width: 50%;
  opacity: 0;
  transform: translateY(40px);
  transition: all 0.6s linear;
}

.tlcontainer.show-animation {
  opacity: 1;
  transform: translateY(0);
}

.text-box {
  padding: 20px 30px;
  /* background-color: #38bdf8; */
  position: relative;
  border-radius: 6px;
}

.left-container {
  left: 0;
}

.right-container {
  left: 50%;
}

.tlcontainer .circle {
  position: absolute;
  width: 30px;
  height: 30px;
  text-align: center;
  border-radius: 50%;
  right: -12px;
  top: 38px;
  z-index: 20;
  color: white;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: #395886;
}

.right-container .circle {
  left: -17px;
}

.timeline::after {
  content: '';
  position: absolute;
  width: 2px;
  height: 100%;
  background-color: #FFFFFF99;
  box-shadow: 0 0 20px 1px rgb(63, 63, 63);
  left: 50%;
  top: 0;
  margin-left: -3px;
  z-index: -1;
  animation: moveline 4s linear forwards;
}

@keyframes moveline {
  0% {
    height: 0;
  }

  100% {
    height: 100%;
  }
}

.text-box h2 {
  font-weight: 600;
}

.left-container-arrow {
  height: 0;
  width: 0;
  position: absolute;
  top: 28px;
  z-index: 1;
  border-top: 15px solid transparent;
  border-bottom: 15px solid transparent;
  border-left: 15px solid #93C5FD;
  right: -15px;
}

.right-container-arrow {
  height: 0;
  width: 0;
  position: absolute;
  top: 28px;
  z-index: 1;
  border-top: 15px solid transparent;
  border-bottom: 15px solid transparent;
  border-right: 15px solid #93C5FD;
  left: -15px;
}

/* Mobile Responsive */
@media screen and (max-width: 600px) {
  .text-box {
    padding: 20px 20px;
  }

  .timeline {
    margin: 20px auto;
  }

  .timeline::after {
    left: 20px;
  }

  .tlcontainer {
    width: 100%;
    padding-left: 55px;
    padding-right: 0px;
  }

  .tlcontainer .circle {
    right: -20px;
  }

  .right-container {
    left: 0;
  }

  .left-container .circle,
  .right-container .circle {
    left: 3px;
  }

  .left-container-arrow,
  .right-container-arrow {
    border-right: 15px solid #93C5FD;
    border-left: 0;
    left: -15px;
  }
}
</style>
