<template>
  <div class="timer-container">
    <div class="timer" :style="{ marginLeft: `${percentage}%` }"></div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted, computed, defineEmits } from 'vue'


const props = defineProps({
  time: {
    type: Number,
    required: true,
  }
})

let timer = null
const timeLeft = ref(props.time)
const percentage = computed(() => ((timeLeft.value / props.time) * 100))
const timeOut = defineEmits(['timeOut'])

onMounted(() => {
  timer = setInterval(() => {
    if (timeLeft.value > 0) {
      timeLeft.value--
    } else {
      clearInterval(timer)
      timeOut('timeOut')
    }
  }, 1000)
})

onUnmounted(() => {
  clearInterval(timer)
})
</script>

<style scoped>
.timer-container {
  width: 100%;
  height: 20px;
  background: linear-gradient(to right, red, yellow, green);
  border-radius: 10px;
  overflow: hidden;
}

.timer {
  width: 100%;
  height: 100%;
  background-color: #fff;
  transition: margin-left 1s linear;
}
</style>
