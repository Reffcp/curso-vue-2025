<script setup>
defineProps({
  titulo: String,
  contenido: String,
  image: String,
})
</script>

<template>
  <div class="card" style="width: 18rem">
    <img :src="image" class="card-img-top" alt="..." />
    <div class="card-body">
      <h5 class="card-title">{{ titulo }}</h5>
      <p class="card-text">
        {{ contenido }}
      </p>
    </div>
  </div>
</template>

<style scoped></style>
