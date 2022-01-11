<template>
  <button @click="$emit('turnTrigger')">Начать игру</button>
</template>

<script>
export default {
  name: 'StartButtonComponent',
  methods: {
  },
  data () {
    return {
    }
  }
}
</script>

<style scoped>
</style>
