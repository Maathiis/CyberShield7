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
  <div v-if="character"> <!-- Affiche uniquement si le personnage est trouvé -->
    <img :src="`/backgrounds/${character.image}`" alt="Image de la famille" />
    <div>Rôle : {{ character.role }}</div> <!-- Rôle -->
    <div>Famille : {{ character.family }}</div> <!-- Famille -->
    <div>Nom : {{ character.name }}</div> <!-- Nom -->
    <div>Définition : {{ character.definition }}</div> <!-- Définition -->
  </div>
  <div v-else>
    <p>Personnage non trouvé.</p> <!-- Message si aucun personnage n'est trouvé -->
  </div>
</template>
