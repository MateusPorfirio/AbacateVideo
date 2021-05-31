<template>
  <button 
    ref="playPause"
    @click="() => status = !status"></button>
</template>

<script>
export default {
  name: 'ButtonPlayPause',

  props: {
    value: {
      type: Boolean,
      default: false
    }
  },

  data() {
    return {
      status: false
    }
  },
  watch: {
    status(val) {
      const button = this.$refs.playPause;
      val ? button.classList.add('play') : button.classList.remove('play'); 
      this.$emit('input', val);
    },

    value(val) {
      this.status = val;
    }
  }
}
</script>

<style scoped>
button {
  height: 100px;
  width: 100px;
  cursor: pointer;
  background-color: transparent;
  background-image: url("../assets/button_pause.png");
}

.play {
  background-image: url("../assets/button_play.png");
}
</style>