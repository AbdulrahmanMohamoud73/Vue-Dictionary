<script setup>
const props = defineProps({
  results: Array,
});
  let audioExists = props.results[0].phonetics

function audioplay () {
  let obj = props.results[0].phonetics.find(o => o.audio !== "")
if (obj) {
  let audio = new Audio(obj.audio);
  audio.play();
}

}
</script>

<template>
  <main>
    <article class="definitionContainer">
      <div class="wordandsound">
      <h2 class="word">{{ results[0].word }}</h2>
      <button v-if='audioExists' @click="audioplay" type="button"><i class="fa-solid fa-volume-high fa-2xl"></i></button>
      </div>
      <div class="pronunciation">{{ results[0].phonetic }}</div>
      <div
        v-for="meaning in results[0].meanings"
        :key="results[0].meanings.indexOf(meaning)"
      >
        <div class="partofspeech">({{meaning.partOfSpeech}})</div>
        <div
          class="definition"
          v-for="(definition, index) in meaning.definitions"
          :key="index"
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

.pronunciation {
  margin: 10px 0px;
}

.word {
  font-size: 40px;
  letter-spacing: 2.5px;
}

button {
  border: 0;
  background-color: transparent;
  cursor: pointer;
}


.wordandsound {
  display: flex;
  flex-direction: row;
  justify-content: space-between;

}

.definition {
  font-weight: bold;
  margin: 2em 0;
}

.pronunciation {
  font-size: 14px;
}

.example {
  font-size: 1.2em;
  font-style: italic;
  color: #696969;
  margin: 15px 0px;
  margin-left: 25px;
  border-left: solid 5px;
  padding-left: 10px;
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
