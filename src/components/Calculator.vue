<template>
  <!-- Input -->
  <div class="input-group">
    <input class="form-control me-3" type="number" name="" id="" />
    <input type="checkbox" name="" id="" />
  </div>
  <div class="input-group">
    <input class="form-control me-3" type="number" name="" id="" />
    <input type="checkbox" name="" id="" />
  </div>
  <div class="input-group">
    <input class="form-control me-3" type="number" name="" id="" />
    <input type="checkbox" name="" id="" />
  </div>

  <!-- Operator -->
  <div class="operator-group">
    <button class="operator-btn">+</button>
    <button class="operator-btn">-</button>
    <button class="operator-btn">x</button>
    <button class="operator-btn">/</button>
  </div>

  <hr />

  <div class="result-box">
    <p>Hasil</p>
    <p>1</p>
  </div>
</template>

<script>
export default {
  name: 'Calculator',
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
