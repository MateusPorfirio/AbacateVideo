<template>
  <div>
    <img :src="images[image]"/>
    
    <input 
      type="range"
      min="0"
      max="1"
      step="0.1"
      v-model="volume"/>
    
    <p>{{total}}</p>
  </div>
</template>

<script>
import soundOff from '../assets/sound_off.png'
import soundMin from '../assets/soud_medium.png'
import soundMax from '../assets/sound_max.png'

export default {
  name: 'InputVolume',
  
  props: {
    value: {
      type: Number
    }
  },

  data() {
    return {
      volume: 1,
      image: 2,
      images: [soundOff, soundMin, soundMax]
    }
  },

  computed: {
    total() {
      const tot = this.volume * 100;
      return `${tot}%`;
    }
  },

  watch: {
    volume(val) {
      this.$emit('input', val);

      if (val <= 0.5 && val > 0) this.image = 1;
      else if (val > 0.5) this.image = 2;
      else this.image = 0;
    },
    value(val) {
      this.volume = val;
    }
  }
}
</script>

<style scoped>
div {
  /* background-color: blue; */
  height: 50%;
  width: 35%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 30px;
}
  div img {
    height: 30px;
    width: 30px;
  }
  div input {
    width: 220px;
  }
  div p {
    color: white;
    font-family: 'Roboto', sans-serif;
  }

</style>