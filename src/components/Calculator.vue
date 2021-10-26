<template>
    <div>
        <input type="number" v-model.number="operand1" placeholder="operand1">
        <input type="number" 
        v-model.number="operand2" 
        placeholder="operand2" 
        @blur="sendData(operand2)"/>
        = {{sum}}
        <div class="keyboard">
            <button v-on:click="sum = operand1 + operand2">+</button>
            <button @click="sum = operand1 - operand2">-</button>
            <button @click="mult">*</button>
            <button @click="div(operand1, operand2)">/</button>
            <button @click="divTwo(operand1, operand2)">%</button>
            <button @click="exponentiation(operand1, operand2)">^</button>
        </div>
        {{powWithOperand}}
        {{powSum}}
    </div>
</template>

<script>
export default {
    name: "Calculator",
    data(){
        return{
            operand1: 0,
            operand2: 0,
            sum: 0,
        }
    },
    //watch позволяет увидеть изменения (новое значение и старое) СМОТРИТ за изменениями
    watch: {
        sum: function(newValue, oldValue){
            // this.sum = this.sum + 1 (будет цикл, т.к. после изменения сумма увеличивается на 1(еще раз меняется))
            console.log(newValue, oldValue);
            this.sendData(newValue);
        }
    },
    methods: {
        mult(){
            this.sum = this.operand1 * this.operand2;
        },
        div(op1, op2){
            this.sum = op1/op2;
        },
        sendData(data){
            console.log('Send Data name', data);
        },
        divTwo(op1, op2){
            this.sum = Math.floor(op1 / op2);
        },
        exponentiation(op1, op2){
            this.sum = Math.pow(op1,op2);
        }
    },
    //ВЫЧИСЛЯЕТ значения после действий пользователя(?)
    computed: {
        powWithOperand(){
            return Math.pow(this.operand1, this.operand2);
        },
        powSum(){
            return Math.pow(this.sum, 4);
        }
    }
}
</script>

<style>
input{
    font-weight: bold;
    color: rgb(29, 113, 134);
}
</style>