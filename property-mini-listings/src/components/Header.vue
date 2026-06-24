<template>
  <header>
    <h1>Homes & Beyond</h1>
    <p>Total Properties: {{ propertyCount }}</p>
  </header>
</template>

<script setup>
defineProps({
  propertyCount: Number
})
</script>

<style scoped>
header {
  background-color: #094931;
  color: white;
  text-align: center;
  padding: 20px;
}

p {
  margin-top: 10px;
}
</style>