<template>
  <div class="cell">
    <slot />
  </div>
</template>

<style scoped>
  .cell {
    width: 100px;
    border: 1px solid #cccccc;
    text-align: center;
    display: flex;
    justify-content: center;
    height: 100px;
    align-items: center;
    font-family: sans-serif;
    font-size: 38px;
    color: #4f4f4f;
    cursor: pointer;
  }
</style>
