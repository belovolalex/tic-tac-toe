<template>
  <modal
    :name="modalName"
    @before-open="beforeOpen"
    @before-close="beforeClose"
    :adaptive="true"
    :click-to-close="false"
    classes="vm--modal"
  >
    <p>{{ result }}</p>
    <StartButton @onClick="$emit('startNewGame')" />
  </modal>
</template>

<script>
  import StartButton from './StartButton'

  export default {
    components: { StartButton },
    props: {
      modalName: {
        type: String,
        required: true
      }
    },
    data() {
      return {
        result: ''
      }
    },
    methods: {
      beforeOpen(event) {
        this.result = event.params.result
      },
      beforeClose(event) {
        this.$emit('beforeClose', event)
      }
    }
  }
</script>

<style>
  .vm--modal {
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
  }
</style>
