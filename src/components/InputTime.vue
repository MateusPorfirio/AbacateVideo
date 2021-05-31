<template>
  <div>
    <p>{{convert(totalTime)}}</p>
   
    <input 
      type="range"
      min="0"
      :max="totalTime"
      v-model="dataTime"
      step="0.01"
      @change="change"/>
    
    <p>{{atualTime}}</p>
  </div>
</template>

<script>
export default {
  name: 'InputTime',
  
  props: {
    totalTime: {
      type: Number,
      required: true
    },
    value: {
      type: Number,
    }
  },
  
  data() {
    return {
      dataTime: 0
    }
  },

  methods: {
    convert(val) {
      const minutes = parseInt(`${(val/60)}`);
      const seconds = parseInt(`${(val%60)}`);

      const min = (minutes <= 9) ? `0${minutes}` : minutes.toString();
      const seg = (seconds <= 9) ? `0${seconds}` : seconds.toString();

      return `${min}:${seg}`;
    },

    change() {
      this.$emit('change', this.dataTime);
    }
  },
  
  computed: {
    atualTime() {
      return this.convert(this.dataTime);
    }
  },

  watch: {
    dataTime(val) {
      this.$emit('input', parseFloat(val));
    },
    value(val) {
      this.dataTime = val;
    }
  }
}
</script>

<style scoped>
div {
  height: 50%;
  width: 60%;
  padding: 0 40px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
  div input {
    width: 80%;
  }
  div p {
    font-size: 1.1rem;
    font-family: 'Roboto', sans-serif;
    font-weight: 300;
    color: white;
  }
  div p:first-child {
    font-weight: 600;
  }

</style>