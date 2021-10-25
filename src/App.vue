<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <div v-html="dataHTML"></div>
    <HelloWorld msg="Welcome to Your Vue.js App" :date="computedDate"/>
    <Calculator/>

    <!-- <input @keyup.enter="onEnter"> --> <!-- после нажатия enter выполняется функция onEnter-->
    <input @keyup="onEnter"> <!-- каждый раз при введении выполняется функция onEnter -->

    <!-- <HelloWorld msg="Welcome to Your Vue.js App" :date="currentDate || new Date()"/> -->
    <button @click="onClick">Click me </button> / {{count}}
    <button @click="count = 1 + 2">Sum</button>
    <button @click="onClick2(1,4)">Click me2</button>
    {{ message }}
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import Calculator from './components/Calculator.vue'

export default {
  name: 'App',
  components: {
    HelloWorld,
    Calculator,
  },
  data(){
    return {
      count: 0,
      currentDate: null,
      message: "HI",
      dataHTML: "<div class='data'>123123</div>",
    }
  },
  methods: {
    onClick(){
      this.count +=1;
    },
    onClick2(param, param2){
      this.count = param + param2;
    },
    onEnter(){
      console.log('KeyUp');
    }
  },
  computed: {
    computedDate(){
      return this.currentDate || new Date();
    }
  },
}
</script>

<style >
button {
  background-color: #2c3e50;
  }
.data {
  color: green;
  background-color: aqua;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
