<script setup>
import { ref } from 'vue';
import Card from "../components/Card.vue"

let character = ref([])
let page = ref(1)

function nextPage(){
  page.value++
  loadCharacters()
}

function previousPage(){
  page.value--
  if(page.value<1){
    page.value=1
  }
  loadCharacters()
}

async function loadCharacters(){
  const response = await fetch(`https://rickandmortyapi.com/api/character?page=${page.value}`)
  const data = await response.json()
  character.value = data.results
  console.log(data)
}
loadCharacters()

</script>

<template>
  <div class="flex justify-center mb-12 mt-10">
    <h1 class=" text-3xl md:text-5xl ">Personajes de Rick y Morty</h1>
  </div>


    <div class="flex justify-center items-center m-4 space-x-4">
    <button class="bg-gray-300 rounded-xl text-center p-4" @click="previousPage" :disabled="page===1">Pagina anterior</button>
    <div class="text-3xl">{{ page }}</div>   
    <button  class="bg-gray-300 rounded-xl text-center p-4"  @click="nextPage" >Pagina siguiente</button>
    </div>
   
  <div class="grid gap-4 grid-cols-2 md:grid-cols-3 lg:grid-cols-5  m-6">
  <RouterLink v-for="personaje in character"  :key="character.id" :to="`/${personaje.id}`">
   <Card :character="personaje"></Card>
  </RouterLink>
  </div>
  
  
</template>
