<template>
  <h3>Agregar</h3>
  <form id="form">
    <div class="form-control">
      <label for="text">Titulo</label>
      <input
        type="text"
        id="text"
        v-model="name"
        placeholder="Digita el nombre..."
      />
    </div>

    <div class="form-control">
      <label for="amount">Cantidad<br /></label>
      <input
        type="number"
        id="amount"
        v-model="amount"
        placeholder="Digita el monto..."
      />
    </div>

    <button @click.prevent="handleClick" class="btn">Guardar</button>
  </form>
</template>

<script setup>
import { ref } from 'vue'
import { useToast } from 'vue-toastification'

const name = ref(null)
const amount = ref(null)

const emit = defineEmits(['updateArray'])

const toast = useToast()

const handleClick = () => {
  if (!name.value || !amount.value) {
    toast.error('Los dos campos son requeridos')
    return
  }

  const transactionData = {
    name: name.value,
    amount: parseFloat(amount.value)
  }

  emit('updateArray', transactionData)

  name.value = null
  amount.value = null
}
</script>

<style scoped></style>
