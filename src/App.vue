<template>
  <div id="app">
    <Calculator/>

    <hr/>

    <counter v-if="showCounterValue" @click="showCounter" ref="counter"/>
    <button @click="showCounter">Change</button>

  </div>
</template>

<script>
import Calculator from './components/Calculator.vue'
import Counter from './components/Counter.vue';

export default {
  name: 'App',
  components: {
    Calculator,
    Counter,
  },
  data(){
    return {
      showCounterValue: true,
      // count: 0,
      // currentDate: null,
      // message: "HI",
      // dataHTML: "<div class='data'>123123</div>",
    }
  },
  methods: {
    showCounter(){
      this.$refs.counter.onClick;
      console.log(this.$refs.counter.counter) //$refs помогает получить доступ к методам и свойствам компонентов
    },
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
