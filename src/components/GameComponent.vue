<template>
  <div class="column">
    <div class="row">
      <game-button id="one" @click="theGame('one')" light-color="#44836b" standard-color="aquamarine" :lightning="buttonsHighlight.one"/>
      <game-button id="two" @click="theGame('two')" light-color="#764e9b" standard-color="#c17fff" :lightning="buttonsHighlight.two"/>
    </div>
    <div class="row">
      <game-button id="three" @click="theGame('three')" light-color="#9b8f4e" standard-color="#ffea7f" :lightning="buttonsHighlight.three"/>
      <game-button id="four" @click="theGame('four')" light-color="#ad5658" standard-color="#ff7f83" :lightning="buttonsHighlight.four"/>
    </div>
  </div>
</template>

<script>
import GameButton from './GameButton'

const set = ['one', 'two', 'three', 'four']

export default {
  name: 'ButtonComponent',
  components: { GameButton },
  emits: ['notifyResult'],
  data () {
    return {
      buttonsHighlight: {
        one: false,
        two: false,
        three: false,
        four: false
      },
      myexpect: [],
      myTrigger: false,
      clickedButton: '',
      counter: 0,
      score: 0
    }
  },
  props: {
    trigger: Boolean
  },
  methods: {
    gameHardRound (timer) {
      this.addElement()
      this.myexpect.forEach((item) => {
        switch (item) {
          case 'one':
            setTimeout(() => { this.buttonsHighlight.one = true }, timer = timer + 400)
            setTimeout(() => { this.buttonsHighlight.one = false }, timer = timer + 400)
            break
          case 'two':
            setTimeout(() => { this.buttonsHighlight.two = true }, timer = timer + 400)
            setTimeout(() => { this.buttonsHighlight.two = false }, timer = timer + 400)
            break
          case 'three':
            setTimeout(() => { this.buttonsHighlight.three = true }, timer = timer + 400)
            setTimeout(() => { this.buttonsHighlight.three = false }, timer = timer + 400)
            break
          case 'four':
            setTimeout(() => { this.buttonsHighlight.four = true }, timer = timer + 400)
            setTimeout(() => { this.buttonsHighlight.four = false }, timer = timer + 400)
            break
        }
      })
    },
    addElement () {
      this.myexpect.push(set[Math.ceil(Math.random() * 4 - 1)])
    },
    theGame (clickedButton) {
      if (clickedButton === this.myexpect[this.counter]) {
        if (this.counter + 1 === this.myexpect.length) {
          this.score = this.score + 1
          this.counter = 0
          // блокируем кнопки
          this.gameHardRound(0)
          this.$emit('notifyResult', this.score)
        }
        this.counter = this.counter + 1
      } else {
        this.score = 0
        this.counter = 0
        this.myexpect = []
        this.$emit('notifyResult', 'Вы проиграли')
      }
    }
  },
  watch: {
    trigger: function () {
      this.gameHardRound(0)
    }
  }
}
</script>

<style lang="scss" scoped>
@import "../assets/commonStyles";
#one {
  border-radius: 100% 0 0 0;
}
#two {
  border-radius: 0 100% 0 0 ;
}
#three {
  border-radius: 0 0 0 100%;
}
#four {
  border-radius: 0 0 100% 0 ;
}
</style>
