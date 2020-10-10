<template>
  <div id="app">
    <transition name="fade" mode="out-in">
      <Start
        v-if="!start"
        @onStart="start = true"
      />
      <div v-else class="wrapper-cells">
        <Cells />
      </div>
    </transition>
  </div>
</template>

<script>
import Cells from './components/Cells'
import Start from './components/Start'

export default {
  name: 'App',
  components: {
    Start,
    Cells
  },
  data() {
    return {
      start: false
    }
  }
}
</script>

<style scoped>
  .wrapper-cells {
    height: 100vh;
    display: flex;
  }
</style>
