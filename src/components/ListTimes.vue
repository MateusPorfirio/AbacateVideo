<template>
  <div>
    <h1>Lista de tempos</h1>
    <ul>
      <li 
        :key="index" 
        v-for="(item, index) in times"
        @click="sendTime(item)">

        {{`${item.time} - ${item.description}`}}
      </li>
    </ul>
  </div>
</template>

<script>
import times from '../assets/times.js'

export default {
  name: 'ListTimes',
  data() {
    return {
      times
    }
  },
  methods: {
    sendTime({ time }) {
      this.$emit('click', time);
    }
  }
}
</script>

<style scoped>
div {
  height: 100%;
  width: 100%;
  /* background-color: red; */
  display: flex;
  flex-direction: column;
  align-items: center;
  font-family: 'Roboto', sans-serif;
}
  div h1 {
    font-size: 1.5rem;
    font-weight: 400;
    color: white;
  }
  div ul {
    /* background-color: blue; */
    height: 100%;
    width: 100%;
    padding: 20px;
  }

  div ul li {
    /* background-color: red; */
    height: 30px;
    display: flex;
    justify-content: center;
    align-items: center;
    margin-bottom: 5px;
    cursor: pointer;
    color: white;
  }
  div ul li:hover {
    color: #00a8ff;
  }

</style>