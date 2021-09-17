<template>
  <!-- Input -->
  <div v-for="input in inputs" :key="input.id" class="input-group">
    <input
      v-model.number="input.value"
      class="form-control me-3"
      type="number"
    />
    <input v-model="input.isActive" type="checkbox" />
  </div>

  <!-- Operator -->
  <div class="operator-group">
    <button
      v-for="operation in operations"
      :key="operation.name"
      @click="calculateResult(operation.name)"
      class="operator-btn"
    >
      {{ operation.sign }}
    </button>
  </div>

  <hr />

  <p class="error-message" v-if="hasError">{{ errorMessage }}</p>

  <div class="result-box">
    <p>Hasil</p>
    <p>{{ calcResult }}</p>
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
      errorMessage: 'Err: Two active inputs required.',

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
    calcResult() {
      return this.selectedOperation ? this[this.selectedOperation] : 0;
    },

  },

  methods: {
    setOperator(operator) {
      this.selectedOperation = operator;
    },

    calculateResult(operation) {
      this.setOperator(operation);

      this.hasError = this.calculatedInputs.length < 2;

      this.result = this[operation];
    },
  },
};
</script>

<style>
  .input-group {
    display: flex;
    margin-bottom: 0.75rem;
  }

  .input-group .form-control {
    width: 100%;
    padding: 0.5rem;
  }

  .operator-group {
    display: flex;
    justify-content: space-between;
    margin-top: 2rem;
    margin-bottom: 2rem;
  }

  .operator-btn {
    width: 3rem;
    height: 3rem;
  }

  .result-box {
    display: flex;
    justify-content: space-between;
  }

  .me-3 {
    margin-right: 1rem;
  }
</style>
