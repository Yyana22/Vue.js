<template>
  <div id="app">
    <div :class="[$style.header]">
      <h1>My Personal Cost</h1>
    </div>
    <div class="wrapper">
      <AddPaymentForm @addNewPayment="addNewPaymentData"/>
      <br>
      <button @click="paymentsDisplayFlagChange()">ADD NEW COST+</button>
      <PaymentsDisplay v-show="paymentsDisplayFlag" :items="paymentsList"/>
    </div>
  </div>
</template>

<script>
import PaymentsDisplay from './components/PaymentsDisplay.vue'
import AddPaymentForm from './components/AddPaymentForm.vue'
export default {
  name: 'App',
  components: {
    PaymentsDisplay,
    AddPaymentForm,
  },
  paymentsDisplayFlag: '',
  data(){
      return {
          paymentsDisplayFlag: '',
          paymentsList: [],
      }
  },
  methods: {
    paymentsDisplayFlagChange(){
      this.paymentsDisplayFlag = !this.paymentsDisplayFlag;
      console.log(this.paymentsDisplayFlag);
    },
    addNewPaymentData(value){
      this.paymentsList = [...this.paymentsList, value];
    },
      fetchData(){
          return [
              {
                  date: "12.03.2020",
                  category: "food",
                  value: 180,
              },
              {
                  date: "12.04.2020",
                  category: "internet",
                  value: 100,
              },
              {
                  date: "01.02.2010",
                  category: "food",
                  value: 180,
              },
              {
                  date: "03.03.2020",
                  category: "sport",
                  value: 1400,
              },
          ]
      }
  },
    created(){
        this.paymentsList = this.fetchData()
    }
}
</script>

<style module>
.header {
  color: rgb(2, 71, 5);
  font-size: 20px;
}
</style>