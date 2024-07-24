<template>
  <HeaderApp />
  <div class="container">
    <BalanceApp :total="+total" />
    <IncomeExpensesApp :income="+income" :expense="+expense" />
    <TransactionListApp
      :transactions="transactions"
      @transactionDeleted="handleTransactionDeleted"
    />
    <AddTransactionApp @updateArray="handleUpdateArray" />
  </div>
</template>

<script setup>
import HeaderApp from './components/HeaderApp.vue'
import BalanceApp from './components/BalanceApp.vue'
import IncomeExpensesApp from './components/IncomeExpensesApp.vue'
import TransactionListApp from './components/TransactionListApp.vue'
import AddTransactionApp from './components/AddTransactionApp.vue'

import { useToast } from 'vue-toastification'

import { ref, computed, onMounted } from 'vue'

const toast = useToast()

const transactions = ref([])

onMounted(() => {
  const savedTransactions = JSON.parse(localStorage.getItem('transactions'))

  if (savedTransactions) {
    transactions.value = savedTransactions
  }
})

const total = computed(() => {
  return transactions.value
    .reduce((acc, transaction) => {
      return acc + transaction.amount
    }, 0)
    .toFixed(2)
})

const income = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount > 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount
    }, 0)
    .toFixed(2)
})

const expense = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount < 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount
    }, 0)
    .toFixed(2)
})

const handleUpdateArray = (transactionData) => {
  transactions.value.push({
    id: generateUniqueId(),
    name: transactionData.name,
    amount: transactionData.amount
  })
  saveToLocalStorage()
  toast.success('Agregado correctamente')
}

const generateUniqueId = () => {
  return Math.floor(Math.random() * 100000)
}

const handleTransactionDeleted = (id) => {
  transactions.value = transactions.value.filter(
    (transaction) => transaction.id !== id
  )
  saveToLocalStorage()
  toast.success('Eliminado correctamente')
}

const saveToLocalStorage = () => {
  localStorage.setItem('transactions', JSON.stringify(transactions.value))
}
</script>

<style scoped></style>
