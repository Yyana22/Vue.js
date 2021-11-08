<template>
    <div class="payment-form">
        <input type="number" placeholder="Amount" v-model.number="value">
        <input type="text" placeholder="Category" v-model.trim="category">
        <input type="text" placeholder="Data" v-model.trim="date">
        <button @click="onClick">Save</button>
    </div>
</template>

<script>
export default {
    name: "AddPaymentForm",
    data(){
        return {
            value: 0,
            category: '',
            date: ''
        }
    },
    methods: {
        getCurrentDate(){
            const today = new Date();
            const d = today.getDate();
            const m = today.getMonth() + 1;
            const y = today.getFullYear();
            return `${d}.${m}.${y}`
        },
        onClick(){
            console.log('saved');
            const {value, category} = this;
            const data = {
                value, 
                category, 
                date: this.date || this.getCurrentDate,
            }
            console.log(data)
            this.$emit('addNewPayment', data)
        },
    },
}
</script>

<style>

</style>