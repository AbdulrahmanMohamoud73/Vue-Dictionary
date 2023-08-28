<script setup>
import { ref, onMounted } from 'vue';
import DefinitionCard from './DefinitionCard.vue';

let input = ref('');
let results = ref(null);

function apiRes() {
  fetch(`https://api.dictionaryapi.dev/api/v2/entries/en/` + input.value)
    .then((response) => response.json())
    .then((data) => {
      console.log(data);
      results.value = data;
    });
}

onMounted(() => {
  apiRes();
});
</script>

<template>
  <form @submit.prevent="apiRes">
    <label>Online Dictionary</label>
    <div class="searchbar">
      <input type="text" placeholder="Search" v-model="input" />
      <button @click="apiRes" type="button">
        <i class="fa-solid fa-magnifying-glass"></i>
      </button>
    </div>
  </form>
  <DefinitionCard v-if="results" :results="results" />
</template>

<style scoped>
* {
  font-family: 'DM Sans', sans-serif;
}

.searchbar {
  width: 100%;
  max-width: 600px;
  display: flex;
  justify-content: space-evenly;
}

input {
  border: 0;
  max-width: 500px;
  width: 65%;
  height: 2em;
  padding: 4px;
  outline: none;
  border-bottom: solid 0.15em;
}

button {
  height: 2.7em;
  border: 0;
  background-color: transparent;
  cursor: pointer;
}

label {
  font-size: 40px;
  text-align: center;
}

form {
  height: 30%;
  margin: 10px 15%;
  display: flex;
  flex-wrap: wrap;
  flex-direction: column;
  text-align: center;
  justify-content: space-evenly;
  align-content: center;
}
</style>
