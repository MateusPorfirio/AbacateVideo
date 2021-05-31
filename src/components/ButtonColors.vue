<template>
  <div class="button-colors-container">
    <button 
      :key="index" 
      v-for="(btn, index) in buttons"
      @click="trowEvent(btn)">
      <div :class="btn"></div>
      <p> {{btn}} </p>
    </button>
  </div>  
</template>

<script>
export default {
  name: 'ButtonColors',
  data() {
    return {
      buttons: ['colorido', 'monocromo', 'vermelho', 'azul', 'verde']
    }
  },
  methods: {
    trowEvent(button) {
      this.$emit('click', button);
    }
  },
  mounted() {
    this.trowEvent();
  }
}
</script>

<style scoped>
.button-colors-container {
  height: 100%;
  width: 50%;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
}
  button {
    height: 15%;
    width: 100%;
    background-color: transparent;
    display: flex;
    justify-content: flex-start;
    align-items: center;
    cursor: pointer;
    padding-left: 10px;
  }
  button:hover {
    border-radius: 15px;
    border: 1px solid white;
  }
    button div {
      height: 35px;
      width: 35px;
      background-color: black;
      margin-right: 10px;
      border-radius: 10px;
    }
    button p {
      font-size: 0.9rem;
      font-family: 'Roboto', sans-serif;
      font-weight: 600;
      color: white;
    }
    .monocromo {
      background-image: linear-gradient(black, rgb(206, 205, 205)); 
    }
    .colorido { 
      background-image: linear-gradient(#00a8ff, #4cd137, #e84118);
    }
    .vermelho { 
      background-color: #e84118;
    }
    .azul {
      background-color: #00a8ff;
    }
    .verde {
      background-color: #4cd137;
    }

</style>