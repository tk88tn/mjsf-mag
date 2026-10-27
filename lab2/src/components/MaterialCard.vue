<script setup>
defineProps({
  material: {
    type: Object,
    required: true
  },
  selected: {
    type: Boolean,
    default: false
  }
})

const emit = defineEmits(['select'])
</script>

<template>
  <article
    class="material-card"
    :class="{ 'is-selected': selected }"
    @click="emit('select', material.title)"
  >
    <h3>{{ material.title }}</h3>

    <p>{{ material.description }}</p>

    <p>Тема: {{ material.topic }}</p>

    <p>Тривалість: {{ material.minutes }} хв</p>

    <button type="button" @click.stop="emit('select', material.title)">
      Обрати матеріал
    </button>
  </article>
</template>