<template>
    <div class="calculator-container">
        <h1>Calculator       {{value}}</h1>
        <div class="calculator">
            <div class="input-container">
                <input type="text" :value="result" placeholder="Input Number" ref="input" class="calculator-input" readonly/>
                <button class="clear-button" @click="clearInput">Clear</button>
            </div>
            <div class="buttons-grid">
                <button class="number-button" @click="handleClick(1)">1</button>
                <button class="number-button" @click="handleClick(2)">2</button>
                <button class="number-button" @click="handleClick(3)">3</button>
                <button class="number-button" @click="handleClick(4)">4</button>
                <button class="number-button" @click="handleClick(5)">5</button>
                <button class="number-button" @click="handleClick(6)">6</button>
                <button class="number-button" @click="handleClick(7)">7</button>
                <button class="number-button" @click="handleClick(8)">8</button>
                <button class="number-button" @click="handleClick(9)">9</button>
                <button class="number-button" @click="handleClick(0)">0</button>
                <button class="operator-button" @click="handleOperatorClick('+')">+</button>
                <button class="operator-button" @click="handleOperatorClick('-')">-</button>
                <button class="operator-button" @click="handleOperatorClick('*')">*</button>
                <button class="operator-button" @click="handleOperatorClick('/')">/</button>
                <button class="equal-button" @click="calculate">=</button>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'CalculatorPRO',
    data() {
        return {
            result: '',
            calculated:false,
            value: 0
        }
    },
    // watch: {
    //     calculatedValue(oldVal,NewVal){
            

    //     }
    // },
    methods: {
        
        clearInput() {
            this.result = '';
        },
        handleClick(value) {
            if (this.calculated) {
                this.result = value;
                this.calculated = false;
            } else {
                this.result += value;
            }
    },
    handleOperatorClick(operator) {
      // If the last character is an operator, 
      // replace it with the new operator
      if (/[+*/-]$/.test(this.result)) {
        this.result = this.result.slice(0, -1) + operator;
      } else {
        // Otherwise, add the new operator
        this.result += operator;
      }
      this.calculated = false; // Reset flag
    },
    calculate() {
      try {
        let evaluatedResult = eval(this.result.
            replace(/(^|[^0-9])0+(\d+)/g, '$1$2'));
        if (evaluatedResult === Infinity ||
            evaluatedResult === -Infinity) {
          throw new Error('Divide by zero error');
        }
        this.result = Number.isFinite(evaluatedResult)
                      ? evaluatedResult : 'Error';
        this.calculated = true;
        // Set flag to true after calculation
      } catch (error) {
        if (error.message === 'Divide by zero error') {
          this.result = 'Error: Divide by zero';
        } else {
          this.result = 'Error';
        }
    }
}

    }
}
</script>

<style scoped>
.calculator-container {
    max-width: 500px;
    margin: 0 auto;
    padding: 20px;
    background-color: #f4f4f4;
    border-radius: 10px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    text-align: center;
}

h1 {
    font-size: 24px;
    margin-bottom: 20px;
    color: #333;
}

.calculator {
    display: flex;
    flex-direction: column;
    align-items: center;
}

.input-container {
    display: flex;
    width: 100%;
    margin-bottom: 15px;
}

.calculator-input {
    flex: 1;
    padding: 10px;
    font-size: 18px;
    border: 2px solid #ccc;
    border-radius: 5px 0 0 5px;
}

.clear-button {
    padding: 10px 15px;
    font-size: 18px;
    background-color: #dc3545;
    color: white;
    border: 2px solid #ccc;
    border-left: none;
    border-radius: 0 5px 5px 0;
    cursor: pointer;
    transition: background-color 0.3s;
}

.clear-button:hover {
    background-color: #c82333;
}

.buttons-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 15px; /* Increased gap */
    margin-bottom: 15px;
    width: 100%;
}

button {
    padding: 20px 25px; /* Increased padding for wider buttons */
    font-size: 18px;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s;
}

.number-button {
    background-color: #007bff;
    color: white;
}

.operator-button {
    background-color: #28a745;
    color: white;
}

.equal-button {
    background-color: #ffc107;
    color: black;
    grid-column: span 3;
}

button:hover {
    background-color: #0056b3;
}

h4 {
    font-size: 20px;
    color: #333;
    margin-top: 15px;
}
</style>
