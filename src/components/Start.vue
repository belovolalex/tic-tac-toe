<template>
  <section class="start">
    <StartButton @onClick="$emit('onStart')" />
  </section>
</template>

<script>
  import StartButton from './StartButton'

  export default {
    components: { StartButton }
  }
</script>

<style scoped>
  .start {
    width: 100%;
    height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
  }
</style>
