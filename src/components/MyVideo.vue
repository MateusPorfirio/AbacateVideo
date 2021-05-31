<template>
  <div class="video-container">
    <video ref="videoTag"
      @ended="endVideo"
      @timeupdate="updateVideo">
      
      <source 
        :src="midia" 
        type="video/mp4"
        crossOrigin/>
    </video>
  </div>
</template>

<script>
import midia from '../assets/teste.mp4'

export default {
  name: 'MyVideo',
  
  props: {
    playPause: {
      type: Boolean,
      default: false
    },
    value: {
      type: Number,
      default: 0
    },
    update: {
      type: Number,
      default: 0
    },

    volume: {
      type: Number,
      default: 1
    }
  }, 

  methods: {
    endVideo(e) {
      this.$emit('endvideo', e);
    },
    updateVideo() {
      const time = parseInt(`${this.$refs.videoTag.currentTime}`)
      this.time = time;
    }
  },

  data() {
    return {
      midia,
      time: 0
    }
  },

  watch: {
    playPause(val) {
      const video = this.$refs.videoTag;
      val ? video.play() : video.pause();
    },
    time(val) {
      this.$emit('input', val);
    },
    value(val) {
      this.time = val;
    },
    update(val) {
      this.$refs.videoTag.currentTime = val;
    },
    volume(val) {
      this.$refs.videoTag.volume = val;
    }
  }
}
</script>

<style scoped>
.video-container {
  height: 100%;
  width: 100%;
  
  position: relative;
  float: left;

  display: flex;
  justify-content: center;
  align-items: center;
}

  .video-container video {
    height: 99%;
    width: 99%;
  }
</style>