<template>
  <div class="calculator">
    <div class="calculator-input-group">
      <div
        v-for="input in inputs"
        :key="input.id"
        class="calculator-input-item"
      >
        <div style="width: 25%; display: flex; justify-content: center">
          <input v-model="input.isActive" type="checkbox" />
        </div>
        <input
          @focus="$event.target.select()"
          v-model.number="input.value"
          type="number"
        />
      </div>
    </div>
    <div class="calculator-keys">
      <button
        v-for="operation in operations"
        :key="operation.name"
        @click="calculateResult(operation.name)"
        :class="{ 'is-active': selectedOperation === operation.name }"
      >
        {{ operation.sign }}
      </button>
    </div>
    <div class="calculator-display">
      <p class="error-message" v-if="hasError">{{ errorMessage }}</p>
      <span v-if="!hasError">{{ result }}</span>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Calculator',

  data() {
    return {
      inputs: [
        {
          id: 1,
          value: 0,
          isActive: false,
        },
        {
          id: 2,
          value: 0,
          isActive: false,
        },
        {
          id: 5,
          value: 0,
          isActive: false,
        },
      ],

      operations: [
        {
          name: 'addition',
          sign: '+',
        },
        {
          name: 'substraction',
          sign: '-',
        },
        {
          name: 'multiplication',
          sign: '*',
        },
        {
          name: 'division',
          sign: '/',
        },
      ],

      selectedOperation: '',

      hasError: false,
      errorMessage: 'Error: At least two active inputs required.',

      result: 0,
    };
  },

  computed: {
    calculatedInputs() {
      return this.inputs.filter((input) => input.isActive).map((input) => input.value);
    },

    addition() {
      return this.calculatedInputs.length
        ? this.calculatedInputs.reduce((acc, input) => acc + input)
        : 0;
    },

    substraction() {
      return this.calculatedInputs.length
        ? this.calculatedInputs.reduce((acc, input) => acc - input)
        : 0;
    },

    division() {
      return this.calculatedInputs.length
        ? this.calculatedInputs.reduce((acc, input) => acc / input)
        : 0;
    },

    multiplication() {
      return this.calculatedInputs.length
        ? this.calculatedInputs.reduce((acc, input) => acc * input)
        : 0;
    },

  },

  methods: {
    setOperation(operator) {
      this.selectedOperation = operator;
    },

    calculateResult(operation) {
      this.setOperation(operation);

      this.hasError = this.calculatedInputs.length < 2;

      this.result = this[operation];
    },
  },
};
</script>

<style>
  input,
  button {
    border: 0;
    border-radius: 0;
    background-color: transparent;
    outline: none;
  }

  :root {
    font-family: Helvetica, Arial, sans-serif;
  }

  html {
    box-sizing: border-box;
    font-size: 175%;
    font-weight: 300;
    line-height: 1.3;
  }

  body {
    align-items: center;
    display: flex;
    height: 100vh;
    justify-content: center;
  }

  input[type="number"] {
    -webkit-appearance: textfield;
    -moz-appearance: textfield;
    appearance: textfield;
  }
  input[type="number"]::-webkit-inner-spin-button,
  input[type="number"]::-webkit-outer-spin-button {
    -webkit-appearance: none;
  }

  .calculator {
    border-radius: 12px;
    box-shadow: 0 0 40px rgba(0, 0, 0, 0.15);
    margin-left: auto;
    margin-right: auto;
    margin-top: 2rem;
    max-width: 15rem;
  }

  .calculator-input-item {
    display: flex;
    border-bottom: 1px solid #999;
  }

  .calculator-input-item input[type="checkbox"] {
    padding: 0.5rem 0.75rem;
  }

  .calculator-input-item input[type="number"] {
    font-size: 18px;
    text-align: right;
    padding: 0.5rem 0.75rem;
    width: 75%;
  }

  .calculator-display {
    background-color: #222222;
    color: #fff;
    font-size: 1.7rem;
    padding: 0.5rem 0.75rem;
    text-align: right;
    border-bottom-right-radius: 12px;
    border-bottom-left-radius: 12px;
  }

  .calculator-display .error-message {
    font-size: 15px;
    color: rgb(251, 104, 104);
  }

  .calculator-keys {
    background-color: #999;
    display: flex;
    grid-gap: 1px;
  }

  .calculator-keys > *:hover {
    opacity: 0.8;
  }

  .calculator-keys > *.is-active {
    opacity: 0.7;
  }

  .calculator-keys > * {
    background-color: rgb(212, 211, 211);
    padding: 0.5rem 1.25rem;
    position: relative;
    text-align: center;
    width: 25%;
  }
</style>
