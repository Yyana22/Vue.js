<template>
    <div>
        <!-- модификаторы у v-model:
        v-model.number - Для автоматического приведения введённого пользователем к Number,
        v-model.lazy - обновляет данные после завершения ввода
        v-model.trim - автоматически обрезает пробелы в начале и в конце строки
        v-model.number.trim - допустимо
        -->
        <input type="text" v-model.lazy="text1" placeholder="operand0">
        <input type="number" v-model.number="operand1" placeholder="operand1">
        <input type="number" 
        v-model.number="operand2" 
        placeholder="operand2" 
        @blur="sendData(operand2)"/>
        = {{result}}
        <div class="keyboard">
            <button @click="calculate('+')">+</button>
            <button @click="calculate('-')">-</button>
            <button @click="calculate('*')">*</button>
            <button @click="calculate('/')">/</button>
            <button @click="calculate('%')">%</button>
            <button @click="calculate('^')">^</button>
        </div>
    </div>
</template>

<script>
export default {
    name: "Calculator",
    data(){
        return{
            text1: '',
            operand1: 0,
            operand2: 0,
            result: 0,
            error: '',
        }
    },
    //watch позволяет увидеть изменения (новое значение и старое) СМОТРИТ за изменениями
    watch: {
        result: function(newValue, oldValue){
            // this.result = this.result + 1 (будет цикл, т.к. после изменения сумма увеличивается на 1(еще раз меняется))
            console.log(newValue, oldValue);
            this.sendData(newValue);
        }
    },
    methods: {
        calculate(operation = "+"){
            switch(operation){
                case '+':
                    this.add();
                    break;
                case '-':
                    this.substract();
                    break;
                case '*':
                    this.mult();
                    break;
                case '/':
                    this.div();
                    break;
                case '%':
                    this.divTwo();
                    break;
                case '^':
                    this.exponentiation();
                    break;
                default: 
                    break;
            }
        },
        add(){
            this.result = this.operand1 + this.operand2;
        },
        substract(){
            this.result = this.operand1 - this.operand2;
        },
        mult(){
            this.result = this.operand1 * this.operand2;
        },
        div(){

            const {operand1, operand2 } = this;
            if (operand2 === 0){
                return this.result = 'Делить на 0 нельзя'
            }
            this.result = operand1 / operand2;
        },
        divTwo(){
            if(this.operand2 == 0){
                this.result = 'Делить на 0 нельзя';
            } else {
                this.result = Math.floor(this.operand1 / this.operand2);
            }
        },
        exponentiation(){
            this.result = Math.pow(this.operand1, this.operand2);
        },
        sendData(data){
            console.log('Send Data name', data);
        },
    },
    //ВЫЧИСЛЯЕТ значения после действий пользователя(?)
    // computed: {
    //     powWithOperand(){
    //         return Math.pow(this.operand1, this.operand2);
    //     },
    //     powSum(){
    //         return Math.pow(this.result, 4);
    //     }
    // }
}
</script>

<style>
input{
    font-weight: bold;
    color: rgb(29, 113, 134);
}
</style>