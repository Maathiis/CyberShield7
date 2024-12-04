<script setup>
import { onMounted, ref } from 'vue';
import data from '../data/data2.json'; // Assurez-vous du chemin correct
import { useRoute } from 'vue-router';

const route = useRoute();

const character = ref(null); // Initialise character à null
const id = parseInt(route.params.id, 10); // Convertit l'ID de l'URL en nombre

// Cherche le personnage correspondant à l'ID
onMounted(() => {
  console.log("ID dans l'URL :", id);
  const family = data.find((family) => family.Members.some((member) => member.id === id));
  if (family) {
    character.value = family.Members.find((member) => member.id === id);
    character.value.family = family.Family; // Ajoute la famille au personnage
    character.value.image = family.Image; // Ajoute l'image de la famille
  }
  console.log("Personnage trouvé :", character.value);
});
</script>

<template>
  <div v-if="character" class="relative h-screen w-screen">
    <!-- Image de fond -->
    <img 
      :src="`/backgrounds/${character.image}`" 
      class="absolute inset-0 h-full w-full object-cover" 
      alt="Image de la famille" 
    />

    <!-- Contenu textuel positionné -->
    <div class="absolute inset-0 flex flex-col justify-center items-center text-white gap-12">
      <!-- Ligne supérieure -->
      <div class="flex flex-col text-center">
        <div class="font-bold text-5xl">{{ character.role }}</div> <!-- Rôle en haut à droite -->
        <div class="text-base font-bold">Family: {{ character.family }}</div> <!-- Numéro en haut à gauche -->
      </div>

      <!-- Centre -->
      <div class="flex flex-col items-center justify-center space-y-2">
        <div class="font-bold text-2xl mx-12 text-center">{{ character.name }}</div> <!-- Nom au centre -->
        <div class="px-12 text-center leading-relaxed">
          {{ character.definition }}
        </div> <!-- Définition au centre -->
      </div>

      <!-- Bas -->
      <div class="flex justify-center pb-20">
        <div class="text-2xl"></div> <!-- Famille en bas au centre -->
      </div>
    </div>
  </div>
</template>

<style scoped>


</style>