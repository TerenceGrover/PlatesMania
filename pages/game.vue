<template>
  <div class="game-container">
    <Score :score="score" />
    <Timer :time=5 @timeOut="timeOut" :start="!isLoading" />
    <div class="photo-container">
      <div v-if="isLoading">
        ...Loading
      </div>
      <div v-else>
        <Photo :image="result.link" />
      </div>
    </div>
    <div v-if="isLoading">
      ...Loading
    </div>
    <div v-else>
      <Buttons :country="result.country" @add="scorePlus" @sub="fetchPlate" />
    </div>
  </div>
</template>

<script setup>
import Photo from '../components/photo.vue';
import Buttons from '../components/buttons.vue';
import Timer from '../components/timer.vue';
import Score from '../components/score.vue';

const isLoading = ref(true)
const result = ref(null)
const error = ref(null)
const url = 'http://127.0.0.1:5000/api/plate'
const score = ref(0)

const fetchPlate = async () => {
  try {
    isLoading.value = true
    const res = await fetch(url + '/easy')
    if (!res.ok) {
      throw new Error('Failed to fetch')
    }
    result.value = await res.json()
  } catch (err) {
    error.value = err.message
  } finally {
    isLoading.value = false
  }
}

onMounted(async () => {
  await fetchPlate()
})

const scorePlus = () => {
  score.value++
  fetchPlate()
}

const timeOut = async () => {
  console.log('timeOut')
  await fetchPlate()
}

</script>

<style scoped>
.game-container {
  max-width: 100%;
  width: 80vw;
  height: 80vh;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.photo-container {
  max-width: 35vw;
  min-width: 35vw;
  min-height: 40vh;
  display: flex;
  justify-content: center;
  align-items: center;
  border: 2px solid #000000aa;
  border-radius: 10px;
}
</style>