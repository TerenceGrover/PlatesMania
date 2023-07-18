<template>

  <h3>
    Score: {{ props.score }}
  </h3>

</template>

<script setup>
const props = defineProps({
  score: {
    type: Number,
    required: true,
  },
})
</script>