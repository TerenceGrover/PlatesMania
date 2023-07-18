<script setup>

const props = defineProps({
  image: String
})

</script>

<template>
  <div v-if="!props.image">Loading...</div>
  <div class="img-container" v-else>
    <img :src="props.image" />
  </div>
</template>

<style scoped>
  .img-container {
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  img {
    width: 100%;
    height: 100%;
    object-fit: contain;
  }
</style>