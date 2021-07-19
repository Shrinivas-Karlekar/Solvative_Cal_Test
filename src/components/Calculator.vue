<template>
    <div>
        <Heading></Heading>
        <div class="area">
            <div class="output">
                <p>{{operationString}}</p>
                <p>{{ result }}</p>
            </div>
            <div class="calc">
                <div class="btn keys">CE</div>
                <div class="btn keys" @click="clear()">C</div>
                <div class="btn keys">Symbol</div>
                <div class="btn keys" @click="operatorClicked('/')">/</div>

                <div class="btn" @click="numberClicked(7)">7</div>
                <div class="btn" @click="numberClicked(8)">8</div>
                <div class="btn" @click="numberClicked(9)">9</div>
                <div class="btn keys" @click="operatorClicked('*')">*</div>

                <div class="btn" @click="numberClicked(4)">4</div>
                <div class="btn" @click="numberClicked(5)">5</div>
                <div class="btn" @click="numberClicked(6)">6</div>
                <div class="btn keys" @click="operatorClicked('-')">-</div>

                <div class="btn" @click="numberClicked(1)">1</div>
                <div class="btn" @click="numberClicked(2)">2</div>
                <div class="btn" @click="numberClicked(3)">3</div>
                <div class="btn keys" @click="operatorClicked('+')">+</div>
                
                <div class="btn"></div>
                <div class="btn" @click="numberClicked(0)">0</div>
                <div class="btn">.</div>
                <div class="btn keys" @click="operatorClicked('=')">=</div>
            </div>
        </div>
        
    </div>
</template>

<script>
import Heading from "./Heading.vue";
export default {
    name: "Calculator",
    data() {
        return {
            currentValue: 0,
            isValueSaved: false,
            isOperator: false,
            operationString: ''
        }
    },
    components: {
        Heading
    },
    computed: {
        result() {
            return this.isValueSaved ? this.currentValue ? this.currentValue : this.isValueSaved : this.currentValue
        }   
    },
    methods: {
        clear() {
            this.currentValue = 0;
            this.isValueSaved= false;
            this.isOperator = false;
            this.operationString = '';
        },
        numberClicked(number) {
            this.operationString += number;
            if(this.isOperator) {
                this.isValueSaved = false;
            }
            this.currentValue = this.currentValue * 10 + number;
        },
        operatorClicked(operator) {
            this.operationString += operator;
            if(operator) {
                this.calculate();
            }
            else {
                this.isValueSaved = this.currentValue;
            }
            this.currentValue = 0;
            this.isOperator = operator;
        },
        calculate() {
            if(this.operator === '/') {
                this.isValueSaved /= this.currentValue;
            }
            else if(this.operator === '*') {
                this.isValueSaved *= this.currentValue;
            }
            else if(this.operator === '-') {
                this.isValueSaved -= this.currentValue;
            }
            else if(this.operator === '+') {
                this.isValueSaved += this.currentValue;
            }
            else if(this.operator === '=' && this.currentValue) {
                this.isValueSaved = this.currentValue;
            }
            this.currentValue = 0;
            this.isOperator = false;
        }
    }
}
</script>

<style scoped>
body {
    display: grid
}
.area {
    border: 2px solid;
    max-width: 500px;
}
.output {
    box-sizing: border-box;
    justify-content: end;
    padding: 32px;
    display: grid;
    margin: 8px;
}
 .calc {
     display: grid;
     grid-template-columns: repeat(4, minmax(60px, 1fr));
 }
 .keys {
     background: lightgrey;
 }
 .btn {
     cursor: pointer;
     display: grid;
     padding: 15px 10px;
     border-radius: 16px;
     margin-bottom: 2px;
    background: aliceblue;
    margin-right: 1px;
 }
</style>