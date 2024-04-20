<template>
  <div v-if="character" class="about">
    <div class="grid md:grid-cols-1 lg:grid-cols-2 h-screen">
      <div class="m-12">
        <img class="h-full w-full rounded-3xl" :src= character.image alt="">
      </div>
      <div class="flex flex-col items-center justify-center m-12 space-y-5">
        <div class="flex justify-center">
         <h1 class="text-5xl font-bold ">{{ character.name }}</h1>
        </div>
        <div class="flex">
          <Icon class="text-4xl" icon="ph:person-fill" />
          <p class="text-2xl ">Specie{{ character.species }}</p>
        </div>
        <div class="flex"> 
          <Icon class="text-4xl" icon="icons8:gender" />
          <p class="text-2xl ">Gender:{{ character.gender }}</p>
        </div>
        <div class="flex">
          <Icon class="text-4xl" icon="carbon:location-filled" />
          <p class="text-2xl ">Localizacion:{{ character.location.name }}</p>
        </div>
        <div class="flex">
          <Icon class="text-4xl" icon="mdi:world" />
          <p class="text-2xl ">Origin:{{ character.origin.name }}</p>
        </div>
        <div class="flex">
          <Icon class="text-4xl" icon="game-icons:half-dead" />
          <p class="text-2xl ">Status:{{ character.status }}</p>
        </div>
      </div>
    </div>
  </div>
  <Icon icon="mdi-light:home" />
</template>

<script setup> 
 import { useRoute} from 'vue-router';
 import {onMounted, ref} from "vue"
 import { Icon } from '@iconify/vue';
 const character = ref(null)

 const route = useRoute()
 const characterId = route.params.id
 onMounted(async() => {
 try{
  const response = await fetch(`https://rickandmortyapi.com/api/character/${characterId}`)
  const data = await response.json()
  character.value = data
  console.log(data)
 }
 catch{


 }


 })
</script>
