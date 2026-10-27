<script setup>
import { ref, reactive, computed } from 'vue'
import { materials } from '../data/materials.js'
import MaterialCard from './MaterialCard.vue'

const selectedTitle = ref(materials[0]?.title ?? '')

const activeFilters = reactive({
  query: '',
  topic: 'all'
})

const filteredMaterials = computed(() => {
  return materials.filter(material => {
    const matchesQuery = material.title
      .toLowerCase()
      .includes(activeFilters.query.toLowerCase())

    const matchesTopic =
      activeFilters.topic === 'all' ||
      material.topic === activeFilters.topic

    return matchesQuery && matchesTopic
  })
})

const totalMinutes = computed(() =>
  filteredMaterials.value.reduce(
    (sum, material) => sum + material.minutes,
    0
  )
)
</script>

<template>
  <section class="material-catalog">
    <h2>Навчальні матеріали</h2>
        <div class="filters">
            <input
                v-model="activeFilters.query"
                type="search"
            placeholder="Пошук матеріалів..."
        />
  <select v-model="activeFilters.topic">
    <option value="all">Усі теми</option>
    <option value="vue">Vue</option>
    <option value="html">HTML</option>
    <option value="css">CSS</option>
    <option value="javascript">JavaScript</option>
  </select>
</div>

    <p>
      Знайдено: {{ filteredMaterials.length }} ·
      Загальна тривалість: {{ totalMinutes }} хв
    </p>

    <p>Вибраний матеріал: {{ selectedTitle }}</p>
    <div class="materials-grid">
  <MaterialCard
    v-for="material in filteredMaterials"
    :key="material.id"
    :material="material"
    :selected="selectedTitle === material.title"
    @select="selectedTitle = $event"
  />
</div>
    <p v-if="filteredMaterials.length === 0">
          Матеріалів не знайдено.
    </p>
  </section>
</template>