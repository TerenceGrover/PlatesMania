<template>
  <div class="buttons-container">
    <button @click="check" v-for="key,value in countries" :key="key" :data-country="value" class="btn">{{ `${key} ${value}` }}</button>
  </div>
</template>

<script setup>
import {Country} from '../resources/CountryMap.json'
import { defineEmits } from 'vue'

const countries = ref({})

const props = defineProps({
  country: String
})

countries.value[props.country] = Country[props.country]

for (let i = 0; i < 3; i++) {
  const randomCountry = Object.keys(Country)[Math.floor(Math.random() * Object.keys(Country).length)]
  if (randomCountry === props.country) {
    i--
    continue
  }
  countries.value[randomCountry] = Country[randomCountry]
}

const scoreEmit = defineEmits(['add', 'sub'])

const check = (e) => {
  if (e.target.dataset['country'] === props.country) {
    scoreEmit('add')
  } else {
    scoreEmit('sub')
  }
}

</script>

<style scoped>
.buttons-container {
  width: 35vw;
  margin-top: 20px;
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-template-rows: 1fr 1fr;
  gap: 20px;
}

.btn {
  padding: 20px 0;
}
</style>