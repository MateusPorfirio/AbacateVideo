<template>
  <div class="controls-container">
    <div class="name-area">
      <h1> Nome do meu vídeo </h1>
    </div>

    <div class="color-controls-area">
      <ButtonColors/>
    </div>
    
    <div class="play-pause-ara">
      <ButtonPlayPause v-model="statusPlayPause"/>
    </div>
    
    <div class="times-area">
      <ListTimes @click="sendTime"/>
    </div>
    
    <div class="controls-area">
      <!-- vai recerber o slider de tempo e de volume (dois componentes separados) -->
      <InputTime 
        :totalTime="20"
        v-model="time"
        @change="change"/>

      <InputVolume v-model="volume"/>
    </div>
  </div>
</template>

<script>
import ButtonColors from './ButtonColors.vue'
import ButtonPlayPause from './ButtonPlayPause.vue'
import ListTimes from './ListTimes.vue'
import InputTime from './InputTime.vue'
import InputVolume from './InputVolume.vue'

export default {
  name: 'Controls',
  
  components: {
    ButtonColors,
    ButtonPlayPause,
    ListTimes,
    InputTime,
    InputVolume
  },

  props: {
    playPause: {
      type: Boolean,
      default: false
    },
    value: {
      type: Number,
      default: 0
    }
  },

  data() {
    return {
      statusPlayPause: false,
      time: 0,
      volume: 1
    }
  },

  watch: {
    statusPlayPause(val) {
      this.$emit('playPause', val);
    },
    playPause(val) {
      this.statusPlayPause = val;
    },
    time(val) {
      this.$emit('input', val);
    },
    value(val) {
      this.time = val;
    },
    volume(val) {
      this.$emit('volume', val);
    }
  },

  methods: {
    change(val) {
      this.$emit('change', val);
    },
    sendTime(e) {
      const val = parseInt(e.split(':')[1]);
      this.$emit('change', val);
    }
  }
}
</script>

<style scoped>
.controls-container {
  height: 100%;
  width: 100%;
  position: relative;
  top: -100%;
  background-color: rgba(0, 0, 0, 0.9);
  
  display: grid;
  grid-template-rows: 20% 50% 30%;
  grid-template-columns: 35% 30% 35%;
  grid-template-areas: 
    "a a a"
    "b c d"
    "e e e";
}

.name-area, .color-controls-area, .play-pause-ara, .times-area, .controls-area {
  height: 100%;
  width: 100%;
  display: flex;
}

.name-area {
  grid-area: a;
  padding: 0 5%;
  justify-content: flex-start;
  align-items: center;
}

  .name-area h1 {
    font-family: 'Roboto', sans-serif;
    font-weight: 400;
    color: white;
  }

.color-controls-area {
  grid-area: b;
  display: flex;
  justify-content: flex-start;
  align-items: center;
  padding-left: 14%;
}

.play-pause-ara {
  grid-area: c;
  display: flex;
  justify-content: center;
  align-items: center;
}

.times-area {
  grid-area: d;
}

.controls-area {
  grid-area: e;
  display: flex;
  justify-content: space-around;
  align-items: center;
}
</style>