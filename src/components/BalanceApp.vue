<template>
  <h4>Tu Balance</h4>
  <h1 id="balance">${{ total }}</h1>
</template>

<script setup>
const props = defineProps({
  total: {
    type: Number,
    required: true
  }
})
</script>

<style scoped></style>
