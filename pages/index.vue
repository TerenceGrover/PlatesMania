<template>
  <div>
    <h1>
      <i class="fas fa-car"></i>
      {{ 'Licence Plate thingy'.toUpperCase() }}
      <i class="fas fa-car"></i>
    </h1>

    <NuxtLink to="/game">
      <button class="btn">Start</button>
    </NuxtLink>
  </div>
</template>

<style scoped>
div {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
button {
  font-size: xx-large;
}
</style>