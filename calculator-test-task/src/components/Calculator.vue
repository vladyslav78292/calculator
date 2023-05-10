<script>
  export default {
    data () {
      return {
        result: 0,
        temporaryNumber: 0,
        operator: '',
        clearInput: false,
      }
    },

    methods: {
      reverse() {
        this.result = this.result * (-1);
      },

      onePercent() {
        this.result = this.result / 100;
      },

      add(number) {
        if (this.result == 0 || this.clearInput) {
          this.result = '';
          this.clearInput = false;
        }

        this.result += number.toString();
      },

      setOperator(operator) {
        if (this.temporaryNumber != 0) {
          this.compute();
        }

        this.temporaryNumber = this.result;
        this.operator = operator;
        this.clearInput = true;
      },

      compute() {
        let value = 0;
        let firstNum = +this.temporaryNumber;
        let secondNum = +this.result;

        switch(this.operator) {
          case '/':
            value = firstNum / secondNum;
            break;
          case 'x':
            value = secondNum * firstNum;
            break;
          case '+':
            value = firstNum + secondNum;
            break;
          case '-':
            value = firstNum - secondNum;
            break;
          default:
            this.temporaryNumber = 0;
            this.operator = ''
            break;
        }

        this.result = value;
      },

      getResult() {
        this.compute();
        this.temporaryNumber = 0;
        this.operator = '';
      },

      reset() {
        this.temporaryNumber = 0;
        this.result = 0;
      },

      addComma() {
        if (!this.result.includes('.')) {
          this.result += '.';
        }
      },

    }
  }
</script>

<template>
  <div class="calculator">
    <input class="calculator-input" type="text" disabled v-model="result" >

    <div class="calculator-line">
      <p v-if="result != 0 || operator" @click="reset" class="calculator-button button-grey">C</p>
      <p v-else class="calculator-button button-grey">AC</p>
      <p @click="reverse" class="calculator-button button-grey">+/-</p>
      <p @click="onePercent" class="calculator-button button-grey">%</p>
    <p @click="setOperator('/')" class="calculator-button button-orange">/</p>
    </div>
    <div class="calculator-line">
      <p @click="add(7)" class="calculator-button button-dark-grey">7</p>
      <p @click="add(8)" class="calculator-button button-dark-grey">8</p>
      <p @click="add(9)" class="calculator-button button-dark-grey">9</p>
      <p @click="setOperator('x')" class="calculator-button button-orange">x</p>
    </div>
    <div class="calculator-line">
      <p  @click="add(4)" class="calculator-button button-dark-grey">4</p>
      <p  @click="add(5)" class="calculator-button button-dark-grey">5</p>
      <p  @click="add(6)" class="calculator-button button-dark-grey">6</p>
      <p @click="setOperator('-')" class="calculator-button button-orange">-</p>
    </div>
    <div class="calculator-line">
      <p  @click="add(1)" class="calculator-button button-dark-grey">1</p>
      <p  @click="add(2)" class="calculator-button button-dark-grey">2</p>
      <p  @click="add(3)" class="calculator-button button-dark-grey">3</p>
      <p @click="setOperator('+')" class="calculator-button button-orange">+</p>
    </div>
    <div class="calculator-line">
      <p   @click="add(0)" class="calculator-button button-dark-grey big-button">0</p>
      <p @click="addComma" class="calculator-button button-dark-grey">,</p>
      <p @click="getResult" class="calculator-button button-orange">=</p>
    </div>
  </div>
</template>

<style>
  .calculator {
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction:column;
    height: 100vh;
    width: 100vw;
    transform: translateX(-50%);
    font-size: 48px;
    color: white;
    width: 370px;
    position: absolute;
    left: 50%;
  }

  .calculator-input {
    display: block;
    width: calc(100% - 40px);
    height: 75px;
    padding: 5px 20px 0;
    margin-bottom: 10px;
    border: none;
    outline: none;
    background-color: black;
    color: white;
    font-size: 80px;
    text-align: right;
  }

  .calculator-button {
    margin: 10px;
    border-radius: 50%;
    width: 80px;
    height: 80px;
    text-align: center;
    line-height: 80px;
    cursor: pointer;
  }

  .big-button {
    border-radius: 48px;
    width: 160px;
    padding-left: 20px;
    text-align: start;
  }

  .button-grey {
    background-color: gray;
    color: white;
  }

  .button-grey:hover {
    background-color: #ddd;
  }

  .calculator-line {
    display: flex;
  }

  .button-dark-grey {
    background-color: #252525;
    color: white;
  }

  .button-orange {
    background-color: #e08d1f;
    color: white;
  }

  .button-orange:hover {
    background-color: #fda22b;
  }
</style>
