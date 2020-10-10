<template>
  <button
    class="start-button"
    @click="$emit('onClick')"
  >
    Start a new game
  </button>
</template>

<script>
  export default {

  }
</script>

<style scoped>
  .start-button {
    outline: none;
    border: none;
    padding: 18px 55px;
    border-radius: 5px;
    cursor: pointer;
    background: #eeeeee;
  }
  .start-button:active {
    border: 1px solid #c4c4c4;
  }
</style>
