<template>
  <div class="timer-container">
    <div class="timer" :style="{ marginLeft: `${percentage}%` }"></div>
  </div>
</template>

<script setup>
import { ref, watchEffect, computed, defineEmits } from 'vue'

const props = defineProps({
  time: {
    type: Number,
    required: true,
  },
  start: {
    type: Boolean,
    required: true,
  },
})

const timeLeft = ref(props.time)
const init = ref(props.start)
const percentage = computed(() => ((timeLeft.value / props.time) * 100))
const timeOut = defineEmits(['timeOut'])

let intervalId = null
const timer = () => {
  intervalId = setInterval(() => {
    if (timeLeft.value > 0) {
      timeLeft.value--
    } else {
      timeOut('timeOut')
      clearInterval(intervalId)
    }
  }, 1000)
  return intervalId
}

watchEffect(() => {
  if (props.start && !init.value) {
    init.value = true
    timeLeft.value = props.time
    timer()
  } else if (!props.start && init.value) {
    init.value = false
    timeLeft.value = props.time
    clearInterval(intervalId)
  }
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
