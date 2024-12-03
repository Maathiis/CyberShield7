<script setup>
import data from '../data/data2.json'
import {onMounted, ref} from "vue";

const characters = ref({});

onMounted(() => {
  characters.value = data
})

</script>

<template>
  <main>
    <h1>CyberShield 7</h1>
    <div class="families">
      <div v-for='families in characters' class="family"
           :style="`background-image: url(/backgrounds/${families.Image})`">
        <h2 class="family-title">{{ families.Family }}</h2>
        <ul class="members">
          <li v-for="members in families.Members" :key="members.id" class="member">
            <a :href="`definition/${members.id}`" class="member-link">{{ members.name }}</a>
          </li>
        </ul>
      </div>
    </div>
  </main>
</template>

<style scoped>

h1{
  text-align: center;
}


/* Main container */
.families {
  display: flex;
  flex-wrap: wrap;
  gap: 2rem;
  padding: 1rem;
}

/* Each family section */
.family {
  border: 1px solid #ddd;
  border-radius: 8px;
  padding: 1rem;
  flex: 1 1 calc(30% - 2rem);
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  position: relative;
  z-index: 1;
}

.family-bg{
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
}

.family:hover {
  transform: scale(1.05);
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.15);
}

/* Family title */
.family-title {
  font-size: 1.5rem;
  color: #ffffff;
  text-align: center;
  margin-bottom: 1rem;
  z-index: 1;
}

/* Member list */
.members {
  list-style: none;
  padding: 0;
  margin: 0;
}

.member {
  margin: 0.5rem 0;
  font-size: 1rem;
}

.member-link {
  text-decoration: none;
  color: #007bff;
  font-weight: bold;
  transition: color 0.3s ease;
}

.member-link:hover {
  color: #0056b3;
  text-decoration: underline;
}
</style>