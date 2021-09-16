<template>
  <!-- Input -->
  <div v-for="input in inputs" :key="input.id" class="input-group">
    <input
      v-model.number="input.value"
      class="form-control me-3"
      type="number"
      name=""
      id=""
    />
    <input type="checkbox" name="" id="" />
  </div>

  <!-- Operator -->
  <div class="operator-group">
    <button @click="setOperator('addition')" class="operator-btn">+</button>
    <button @click="setOperator('substraction')" class="operator-btn">-</button>
    <button @click="setOperator('multiplication')" class="operator-btn">
      x
    </button>
    <button @click="setOperator('division')" class="operator-btn">/</button>
  </div>

  <hr />

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
        },
        {
          id: 2,
          value: 0,
        },
        {
          id: 5,
          value: 0,
        },
      ],

      selectedOperator: '',
    };
  },

  computed: {

    variables() {
      return this.inputs.map((input) => input.value);
    },

    addition() {
      return this.variables.reduce((acc, input) => acc + input);
    },

    substraction() {
      return this.variables.reduce((acc, input) => acc - input);
    },

    division() {
      return this.variables.reduce((acc, input) => acc / input);
    },

    multiplication() {
      return this.variables.reduce((acc, input) => acc * input);
    },

    calcResult() {
      return this.selectedOperator ? this[this.selectedOperator] : 0;
    },

  },

  methods: {
    setOperator(operator) {
      this.selectedOperator = operator;
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
