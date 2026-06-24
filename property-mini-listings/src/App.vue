<script setup>
import { ref, computed } from 'vue'
import Header from './components/Header.vue'
import PropertyCard from './components/PropertyCard.vue'

const properties = ref([
  {
    id: 1,
    title: 'Modern Apartment',
    location: 'Cape Town',
    price: 2500,
    type: 'Apartment',
    image: 'https://rentalrealestate.com/wp-content/uploads/student-housing-investing-1024x576.png',
    available: true,
    favourite: false
  },
  {
    id: 2,
    title: 'Beach House',
    location: 'Camps Bay',
    price: 5500,
    type: 'House',
    image: 'https://www.abdesignstudioinc.com/hs-fs/hubfs/Modern_Beach_House_Montecito_Hero@2x.jpg?width=1920&name=Modern_Beach_House_Montecito_Hero@2x.jpg',
    available: false,
    favourite: false
  },
  {
    id: 3,
    title: 'Luxury Villa',
    location: 'Sea Point',
    price: 8000,
    type: 'Villa',
    image: 'https://tse1.mm.bing.net/th/id/OIP.qQmRhIVyYAOncVqOgD-1MQHaE8?r=0&rs=1&pid=ImgDetMain&o=7&rm=3',
    available: true,
    favourite: false
  },
  {
    id: 4,
    title: 'Studio Apartment',
    location: 'Woodstock',
    price: 1800,
    type: 'Apartment',
    image: 'https://tse1.mm.bing.net/th/id/OIP.6Y0rpwmx6kGIqCu1gIh_YwHaEo?r=0&rs=1&pid=ImgDetMain&o=7&rm=3',
    available: true,
    favourite: false
  }
])

const searchTerm = ref('')
const sortOrder = ref('low')

const filteredProperties = computed(() => {
  let result = properties.value.filter(property =>
    property.title.toLowerCase().includes(searchTerm.value.toLowerCase()) ||
    property.location.toLowerCase().includes(searchTerm.value.toLowerCase())
  )

  if (sortOrder.value === 'low') {
    result.sort((a, b) => a.price - b.price)
  } else {
    result.sort((a, b) => b.price - a.price)
  }

  return result
})

function toggleFavourite(id) {
  const property = properties.value.find(p => p.id === id)

  if (property) {
    property.favourite = !property.favourite
  }
}
</script>

<template>

  <Header :propertyCount="filteredProperties.length" />

  <div class="controls">

    <input
      v-model="searchTerm"
      placeholder="Search by title or location"
    >

    <select v-model="sortOrder">
      <option value="low">Price: Low to High</option>
      <option value="high">Price: High to Low</option>
    </select>

  </div>

  <div class="grid">

    <PropertyCard
      v-for="property in filteredProperties"
      :key="property.id"
      :property="property"
      @toggleFavourite="toggleFavourite"
    />

  </div>

</template>

<style>
body {
  background: #f4f4f4;
  font-family: Arial, sans-serif;
}

.controls {
  text-align: center;
  margin: 20px;
}

input,
select {
  padding: 10px;
  margin: 10px;
}

.grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 20px;
  padding: 20px;
}
</style>