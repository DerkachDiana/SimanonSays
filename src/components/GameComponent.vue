<template>
  <div class="column">
    <div class="row">
      <game-button id="one" :sound="sound_1" @click="theGame('one')" light-color="#44836b" standard-color="aquamarine" :lightning="buttonsHighlight.one"/>
      <game-button id="two" :sound="sound_2" @click="theGame('two')" light-color="#764e9b" standard-color="#c17fff" :lightning="buttonsHighlight.two"/>
    </div>
    <div class="row">
      <game-button id="three" :sound="sound_3" @click="theGame('three')" light-color="#9b8f4e" standard-color="#ffea7f" :lightning="buttonsHighlight.three"/>
      <game-button id="four"  :sound="sound_4" @click="theGame('four')" light-color="#ad5658" standard-color="#ff7f83" :lightning="buttonsHighlight.four"/>
    </div>
  </div>
</template>

<script>
import sound1 from '../sounds/sounds_1.mp3'
import sound2 from '../sounds/sounds_2.mp3'
import sound3 from '../sounds/sounds_3.mp3'
import sound4 from '../sounds/sounds_4.mp3'
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
      sound_1: sound1,
      sound_2: sound2,
      sound_3: sound3,
      sound_4: sound4,
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
        setTimeout(() => { this.buttonsHighlight[item] = true }, timer = timer + 400)
        setTimeout(() => { this.buttonsHighlight[item] = false }, timer = timer + 400)
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
        } else this.counter = this.counter + 1
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
      this.score = 0
      this.$emit('notifyResult', this.score)
      this.counter = 0
      this.myexpect = []
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
