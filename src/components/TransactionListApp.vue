<template>
  <h3>Historial</h3>
  <ul id="list" class="list">
    <li
      v-for="{ id, name, amount } in transactions"
      :key="id"
      :class="amount > 0 ? 'plus' : 'minus'"
    >
      {{ name }}<span>${{ amount }}</span>
      <button @click="deleteTransaction(id)" class="delete-btn">×</button>
    </li>
  </ul>
</template>

<script setup>
const emit = defineEmits(['transactionDeleted'])

const props = defineProps({
  transactions: {
    type: Array,
    required: true
  }
})

const deleteTransaction = (id) => {
  emit('transactionDeleted', id)
}
</script>

<style scoped></style>
