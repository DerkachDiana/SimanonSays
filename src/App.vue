<template>
  <div class="mycolumn">
    <GameComponent :trigger="trigger" @notifyResult="this.score = $event"/>
    <StartButtonComponent @turnTrigger="this.newGame"/>
    <div class="score">{{this.score}}</div>
  </div>
</template>

<script>

import GameComponent from './components/GameComponent'
import StartButtonComponent from './components/StartButtonComponent'
export default {
  name: 'App',
  data () {
    return {
      trigger: false,
      score: 0
    }
  },
  components: {
    StartButtonComponent,
    GameComponent
  },
  methods: {
    newGame () {
      this.trigger = true
      this.score = 0
    }
  },
  computed: {
  }
}
</script>

<style>
.mycolumn {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 25px;
}
</style>
