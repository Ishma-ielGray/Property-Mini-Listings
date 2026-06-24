<template>
  <div class="card">

    <div v-if="!property.available" class="badge">
      Not Available
    </div>

    <img :src="property.image" :alt="property.title">

    <h2>{{ property.title }}</h2>

    <p>📍 {{ property.location }}</p>

    <p>🏠 {{ property.type }}</p>

    <h3>R{{ property.price }}</h3>

    <button @click="$emit('toggleFavourite', property.id)">
      {{ property.favourite ? '★ Favourite' : '☆ Bookmark' }}
    </button>

  </div>
</template>

<script setup>
defineProps({
  property: Object
})
</script>

<style scoped>
.card {
  position: relative;
  background: white;
  padding: 15px;
  border-radius: 10px;
  box-shadow: 0 2px 8px gray;
}

img {
  width: 100%;
  border-radius: 10px;
}

.badge {
  position: absolute;
  top: 10px;
  right: 10px;
  background: rgb(56, 96, 167);
  color: white;
  padding: 5px 10px;
  border-radius: 5px;
}

button {
  margin-top: 10px;
  padding: 10px;
  cursor: pointer;
}
</style>