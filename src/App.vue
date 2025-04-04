<!-- eslint-disable vue/require-v-for-key -->
<script setup>
import { onMounted, ref } from 'vue'
import axios from 'axios'
import ExternalComponent from './components/ExternalComponent.vue'
const datos = ref([])
let pagina = Math.floor(Math.random() * 34 + 1)

onMounted(async () => {
  await getDatos()

  setTimeout(async () => {
    pagina = Math.floor(Math.random() * 34 + 1)
    await getDatos()
  }, 3000)
})

async function getDatos() {
  try {
    const datosTransformados = []
    const respuesta = await axios.get('https://rickandmortyapi.com/api/character/?page=' + pagina)
    //console.log(respuesta.data.results)
    respuesta.data.results.forEach((element) => {
      console.log(element)
      let elementoTemporal = {
        titulo: element.name,
        contenido: element.status,
        imagen: element.image,
      }
      datosTransformados.push(elementoTemporal)
    })
    console.log(datosTransformados)
    datos.value = datosTransformados
    console.log(datos)
  } catch (error) {
    console.log('No se pudo acceder a la librería remota', error.message)
  }
}
</script>

<template>
  <div class="container-expand">
    <div class="row">
      <div v-for="dato in datos" class="col-2">
        <ExternalComponent :image="dato.imagen" :contenido="dato.contenido" :titulo="dato.titulo" />
      </div>
    </div>
  </div>
</template>

<style>
.parrafo {
  color: red;
  font-size: 54px;
}
</style>
