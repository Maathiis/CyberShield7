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
  <div v-if="character" class="relative h-screen w-screen bg-gray-800">
    <!-- Image de fond -->
    <img 
      :src="`/backgrounds/${character.image}`" 
      class="absolute top-0 left-0 w-full h-full object-contain" 
      alt="Image de la famille" 
    />

    <!-- Contenu textuel positionné -->
    <div class="absolute inset-0 flex flex-col text-white">
      <!-- Ligne supérieure -->
      <div class="flex justify-center pt-60">
        <div class="text-5xl font-koulen">{{ character.role }}</div>
        <div class="text-sm italic">FAMILY : {{ character.family }}</div>
      </div>

      <!-- Centre -->
      <div class="flex flex-col items-center justify-center flex-grow space-y-2">
        <div class="mx-20 text-center text-sm leading-relaxed">
          {{ character.definition }}
        </div> <!-- Définition au centre -->
      </div>

      <!-- Bas -->
      <div class="flex pb-6">
        <div class="text-3xl pl-5 pb-44 ">{{ character.name }}</div> <!-- Famille en bas au centre -->
      </div>
    </div>
  </div>
  <div v-else>
    <p>Personnage non trouvé.</p> <!-- Message si aucun personnage n'est trouvé -->
  </div>
</template>

<style scoped>

</style>
