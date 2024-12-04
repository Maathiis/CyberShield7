<script setup>
import data from '../data/data2.json'
import {onMounted, ref} from "vue";

const characters = ref({});

onMounted(() => {
  characters.value = data
})

</script>

<template>
  <div class="sm:grid grid-cols-5 gap-3">

    <div class="h-screen sm:h-full flex flex-col items-center bg-cover bg-center bg-no-repeat px-5 sm:px-10"
         v-for="families in characters"
         :style="`background-image: url(/backgrounds/${families.Image})`"
    >
      <h1 class="text-3xl sm:text-xl font-bold text-center mt-36 sm:mt-10 text-white">{{ families.Family }}</h1>

      <ul class="flex flex-col justify-center mt-5 gap-5">
        <li v-for="member in families.Members">
          <a :href="`/definition/${member.id}`"
             class="text-blue-500 hover:text-blue-600 font-medium underline hover:no-underline transition duration-300 ease-in-out"
          >{{ member.name }}</a>
        </li>
      </ul>

    </div>
  </div>

</template>

