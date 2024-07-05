<template>
  <div class="calculator">
    <div class="display">{{ current }}</div>
    <div class="buttons">
      <button @click="clear">C</button>
      <button @click="appendNumber('7')">7</button>
      <button @click="appendNumber('8')">8</button>
      <button @click="appendNumber('9')">9</button>
      <button @click="chooseOperation('/')">/</button>

      <button @click="appendNumber('4')">4</button>
      <button @click="appendNumber('5')">5</button>
      <button @click="appendNumber('6')">6</button>
      <button @click="chooseOperation('*')">*</button>

      <button @click="appendNumber('1')">1</button>
      <button @click="appendNumber('2')">2</button>
      <button @click="appendNumber('3')">3</button>
      <button @click="chooseOperation('-')">-</button>

      <button @click="appendNumber('0')">0</button>
      <button @click="appendNumber('.')">.</button>
      <button @click="chooseOperation('+')">+</button>
      <button @click="compute">=</button>
    
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      current: '',
      previous: '',
      operation: null
    };
  },
  methods: {
    clear() {
      this.current = '';
      this.previous = '';
      this.operation = null;
    },
    appendNumber(number) {
      if (number === '.' && this.current.includes('.')) return;
      this.current = `${this.current}${number}`;
    },
    chooseOperation(operation) {
      if (this.current === '') return;
      if (this.previous !== '') {
        this.compute();
      }
      this.operation = operation;
      this.previous = this.current;
      this.current = '';
    },
    compute() {
      let computation;
      const prev = parseFloat(this.previous);
      const current = parseFloat(this.current);
      if (isNaN(prev) || isNaN(current)) return;
      switch (this.operation) {
        case '+':
          computation = prev + current;
          break;
        case '-':
          computation = prev - current;
          break;
        case '*':
          computation = prev * current;
          break;
        case '/':
          computation = prev / current;
          break;
        default:
          return;
      }
      this.current = computation;
      this.operation = null;
      this.previous = '';
    }
  }
};
</script>

<style scoped>



.calculator {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  background-color: rgb(255, 0, 212);
  width: 300px;
  height: 300px;
  border-radius: 10%;
}

.display {
  width: 160px;
  height: 40px;
  border: 2px solid rgb(255, 255, 255);
  text-align: right;
  padding: 5px;
  margin-bottom: 10px;
  border-radius: 5%;
  color: rgb(255, 255, 255);
  background-color: rgb(0, 0, 0);
}

.buttons {
  display: grid;
  grid-template-columns: repeat(4, 40px);
  grid-gap: 5px;
  
}

button {
  width: 40px;
  height: 40px;
  font-size: 18px;
  background-color: blueviolet;
  color: rgb(0, 0, 0);
  box-shadow: 2px 2px 2px 1px rgba(0, 0, 0, 0.2);
}


</style>
