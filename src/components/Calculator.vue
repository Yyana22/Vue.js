<template>
    <div>

        <div v-for="(item, idx) in myCollection" :key="`${idx}_parent`"> <!-- при v-for всегда нужен :key -->
            {{ item }} -- {{ idx }}
            <!-- <div v-for="(item, idx) in myCollection[idx]" :key="idx">{{ item }} -- {{ idx }}</div> -->
            </div>

        <div class="logs" v-for="(log, id) in logs" :key="id">{{log}}</div>

        <!-- модификаторы у v-model:
        v-model.number - Для автоматического приведения введённого пользователем к Number,
        v-model.lazy - обновляет данные после завершения ввода
        v-model.trim - автоматически обрезает пробелы в начале и в конце строки
        v-model.number.trim - допустимо
        -->
        <input type="number" v-model.number="operand1" placeholder="operand1">

        <input type="number" 
        v-model.number="operand2" 
        placeholder="operand2" 
        @blur="sendData(operand2)"/>

        <div>= {{result}}</div>
        <div>= fib {{fibResult}}</div>

        <div class="error" 
        :class="{'red': error}" 
        v-if="error">
        {{error}}  
        </div> <!--  каждый раз добавляет\удаляет из DOM дерева элемент, происходят все хуки жизненного цикла --> 

        <div class="error" 
        :class="{'red': error}" 
        v-show="error">
        {{error}}  
        </div> <!--  просто меняет display: none --> 

        <div class="strange-message">
            <template v-if="result <0"> Получилось отрицательное число </template>
            <template v-else-if="result < 100"> Получилось число меньше 100 </template>
            <template v-else>Все остальные числа</template> <!-- v-else не поддерживает условие -->
        </div>

        <div class="keyboard">
            <!-- <button @click="calculate('+')">+</button>
            <button @click="calculate('-')">-</button>
            <button @click="calculate('*')">*</button>
            <button @click="calculate('/')">/</button>
            <button @click="calculate('%')">%</button>
            <button @click="calculate('^')">^</button> -->
            <button v-for="operand in operands" 
                @click="calculate(operand)"
                :key="operand"
                :disabled="operand1 === 0"
                v-bind:title="operand" 
                :alt="operand" 
                > <!-- v-bind связывает шаблон html с данными  :alt - при наведении вылезает картинка(?) с operand'ом
                :disabled, если условие (operand1 === 0) выполняется, уходит возможность взаимодействия с кнопками
                -->
                {{operand}}
            </button>
        </div>
    </div>
</template>

<script>
export default {
    name: "Calculator",
    data(){
        return{
            myCollection: [1,2,3,4,5],
            operands: ['+', '-', '/','*','%','^'],
            text1: '',
            operand1: 0,
            operand2: 0,
            fibResult: 0,
            result: 0,
            error: '',
            logs:{},
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
            this.error = "";
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
            const key = Date.now() // дата в виде мс обозначается
            // this.logs[key] = `${this.operand1}${operation}${this.operand2} = ${this.result}`;
            const value = `${this.operand1}${operation}${this.operand2} = ${this.result}`;
            // Vue.set(object, propertyName, value)
            this.$set(this.logs, key, value);
        },
        add(){
            this.result = this.operand1 + this.operand2;
            this.fibResult = this.fib1 + this.fib2;
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
                return this.error = 'Делить на 0 нельзя'
            }
            this.result = operand1 / operand2;
        },
        divTwo(){
            if(this.operand2 == 0){
                this.error = 'Делить на 0 нельзя';
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
        fib(n){
            return n<=1 ? n : this.fib(n-1) + this.fib(n-2);
        },
    },
    // ВЫЧИСЛЯЕТ значения после действий пользователя(?)
    computed: {
        fib1() {
            return this.fib(this.operand1)
        },
        fib2() {
            return this.fib(this.operand2)
        },
        
        // powWithOperand(){
        //     return Math.pow(this.operand1, this.operand2);
        // },
        // powSum(){
        //     return Math.pow(this.result, 4);
        // }
    }
}
</script>

<style scoped>
.red {
    color: red;
}
input{
    font-weight: bold;
    color: rgb(29, 113, 134);
}
</style>