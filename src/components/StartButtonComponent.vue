<template>
  <button @click="turnOnTrigger">Начать игру</button>
</template>

<script>
export default {
  name: 'StartButtonComponent',
  methods: {
    turnOnTrigger () {
      this.trigger = !this.trigger
      this.$emit('turnTrigger', this.trigger)
    }
  },
  data () {
    return {
      trigger: false
    }
  }
}
</script>

<style scoped>
</style>
