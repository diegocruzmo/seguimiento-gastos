<template>
  <div class="inc-exp-container">
    <div>
      <h4>Entradas</h4>
      <p id="money-plus" class="money plus">${{ income }}</p>
    </div>
    <div>
      <h4>Salidas</h4>
      <p id="money-minus" class="money minus">${{ expense }}</p>
    </div>
  </div>
</template>

<script setup>
const props = defineProps({
  income: {
    type: Number,
    required: true
  },
  expense: {
    type: Number,
    required: true
  }
})
</script>

<style scoped></style>
