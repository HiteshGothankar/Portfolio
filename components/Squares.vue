<template>
  <div class="fixed inset-0 w-screen h-screen pointer-events-none overflow-hidden" 
       :class="zIndexClass" 
       ref="container">
    <div 
      v-for="(square, index) in squares" 
      :key="index"
      class="absolute pointer-events-auto cursor-pointer border transition-colors duration-300"
      :style="getSquareStyle(square, index)"
      @mouseenter="onSquareHover(index)"
      @mouseleave="onSquareLeave(index)"
    ></div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted, nextTick, computed } from 'vue'

const props = defineProps({
  speed: {
    type: Number,
    default: 0.1
  },
  squareSize: {
    type: Number,
    default: 25
  },
  direction: {
    type: String,
    default: 'up',
    validator: (value) => ['up', 'down', 'left', 'right', 'diagonal'].includes(value)
  },
  borderColor: {
    type: String,
    default: '#fff'
  },
  hoverFillColor: {
    type: String,
    default: '#222'
  },
  zIndex: {
    type: String,
    default: '-z-10' // Behind content by default
  }
})

const container = ref(null)
const squares = ref([])
const hoveredSquares = ref(new Set())
const animationId = ref(null)
const startTime = ref(Date.now())
const offsetY = ref(0)

const zIndexClass = computed(() => props.zIndex)

const initializeSquares = () => {
  if (!container.value) return
  
  const containerWidth = window.innerWidth
  const containerHeight = window.innerHeight
  
  // Create connected grid - no gaps between squares
  const cols = Math.ceil(containerWidth / props.squareSize) + 5
  const rows = Math.ceil(containerHeight / props.squareSize) + 8 // Extra rows for continuous movement
  
  squares.value = []
  
  for (let row = 0; row < rows; row++) {
    for (let col = 0; col < cols; col++) {
      squares.value.push({
        gridX: col,
        gridY: row,
        baseX: col * props.squareSize,
        baseY: row * props.squareSize - props.squareSize * 2, // Start above viewport
        // opacity: Math.random() * 0.3 + 0.1,
        opacity:10,
        animationOffset: Math.random() * Math.PI * 2
      })
    }
  }
  
  // console.log(`Initialized ${squares.value.length} connected squares (${cols}x${rows})`)
}

const getSquareStyle = (square, index) => {
  const currentTime = Date.now()
  const elapsed = (currentTime - startTime.value) * props.speed * 0.001
  
  let x = square.baseX
  let y = square.baseY
  
  // Continuous movement based on direction
  switch (props.direction) {
    case 'up':
      y += offsetY.value
      // Reset position when square goes too far up
      if (y < -props.squareSize * 2) {
        y += window.innerHeight + props.squareSize * 4
      }
      break
    case 'down':
      y -= offsetY.value
      if (y > window.innerHeight + props.squareSize) {
        y -= window.innerHeight + props.squareSize * 4
      }
      break
    case 'left':
      x += offsetY.value
      if (x < -props.squareSize * 2) {
        x += window.innerWidth + props.squareSize * 4
      }
      break
    case 'right':
      x -= offsetY.value
      if (x > window.innerWidth + props.squareSize) {
        x -= window.innerWidth + props.squareSize * 4
      }
      break
    case 'diagonal':
      x += offsetY.value * 0.5
      y += offsetY.value
      if (y < -props.squareSize * 2) {
        y += window.innerHeight + props.squareSize * 4
        x = square.baseX
      }
      break
  }
  
  // Subtle opacity animation
  const pulseOpacity = square.opacity + Math.sin(elapsed * 0.5 + square.animationOffset) * 0.1
  const finalOpacity = Math.max(0.05, Math.min(0.4, pulseOpacity))
  
  const isHovered = hoveredSquares.value.has(index)
  
  return {
    left: `${x}px`,
    top: `${y}px`,
    width: `${props.squareSize}px`,
    height: `${props.squareSize}px`,
    borderColor: props.borderColor,
    backgroundColor: isHovered ? props.hoverFillColor : 'transparent',
    opacity: finalOpacity,
    borderWidth: '1px',
    // borderStyle: 'solid'
  }
}

const onSquareHover = (index) => {
  hoveredSquares.value.add(index)
}

const onSquareLeave = (index) => {
  hoveredSquares.value.delete(index)
}

const animate = () => {
  // Continuous movement
  offsetY.value += props.speed * 2
  
  // Reset offset to prevent overflow
  if (offsetY.value > props.squareSize * 2) {
    offsetY.value = 0
  }
  
  // Trigger reactivity
  squares.value = [...squares.value]
  animationId.value = requestAnimationFrame(animate)
}

const handleResize = () => {
  nextTick(() => {
    initializeSquares()
  })
}

onMounted(() => {
  // console.log('Connected Squares component mounted')
  nextTick(() => {
    initializeSquares()
    animate()
    window.addEventListener('resize', handleResize)
  })
})

onUnmounted(() => {
  if (animationId.value) {
    cancelAnimationFrame(animationId.value)
  }
  window.removeEventListener('resize', handleResize)
})
</script>