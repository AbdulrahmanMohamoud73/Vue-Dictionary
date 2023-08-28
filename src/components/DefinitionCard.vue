<script setup>
const props = defineProps({
  results: Array,
});
</script>

<template>
  <main>
    <article class="definitionContainer">
      <h2 class="word">{{ results[0].word }}</h2>
      <div class="pronunciation">{{ results[0].phonetic }}</div>
      <div
        v-for="meaning in results[0].meanings"
        :key="results[0].meanings.indexOf(meaning)"
      >
        <div class="partofspeech">({{meaning.partOfSpeech}})</div>
        <div
          class="definition"
          v-for="(definition, index) in meaning.definitions"
          :key="results[0].meanings.indexOf(definition)"
        >
         {{index + 1}}. {{definition.definition }}
             <div v-if="definition.example" class="example">'{{definition.example}}'</div>
        </div>
      </div>
    </article>
  </main>
</template>

<style scoped>
main {
  display: flex;
  justify-content: center;
  max-width: 1000px;
  margin: 0 auto;
}

.word {
  font-size: 35px;
}

.definition {
  font-weight: bold;
  margin: 2em 0;
}

.pronunciation {
  font-size: 14px;
}

.example {
  font-size: 1.5em;
  font-style: italic;
  color: #696969;
  margin: 10px 0;
}

.definitionContainer {
  min-height: 55vh;
  box-sizing: border-box;
  border-radius: 10px;
  width: 80%;
  max-width: 850px;
  border: solid 0.1em;
  padding: 2em;
  display: flex;
  flex-direction: column;
  justify-content: space-evenly;
  margin-bottom: 20px;
}
</style>
