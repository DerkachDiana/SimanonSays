<template>
  <div class="button" :style="buttonColor"
       @touchstart="lighting" @touchend="returnColor"
       @mousedown="lighting" @mouseup="returnColor" @contextmenu.prevent
  />
</template>

<script>
export default {
  name: 'GameButton',
  data () {
    return {
      isLightning: false,
      isLightningForClick: false
    }
  },
  updated () {
    this.isLightning = this.lightning
  },
  props: {
    lightColor: {
      type: String,
      required: true
    },
    standardColor: {
      type: String,
      required: true
    },
    lightning: {
      type: Boolean,
      default: false
    },
    sound: String
  },
  methods: {
    playSound () {
      const audio = new Audio(this.sound)
      audio.play()
    },
    lighting () {
      this.isLightningForClick = true
      this.playSound()
    },
    returnColor () {
      this.isLightningForClick = false
    }
  },
  computed: {
    buttonColor () {
      return {
        'background-color': this.isLightning || this.isLightningForClick ? this.lightColor : this.standardColor
      }
    }
  },
  watch: {
    lightning (newVal) {
      if (newVal) this.playSound()
    }
  }
}
</script>

<style scoped>
.button {
  width: 100px;
  height: 100px;
}
</style>
