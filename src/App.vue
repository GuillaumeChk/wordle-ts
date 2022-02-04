<template>
  <div>
    <h1>WORDLE</h1>
    <GameGrid :grid="grid" :grid-states="gridStates" />
    <Keyboard @addLetter="addLetter" @validate="validate" @clear="clear" />
    <div class="result" v-if="showResult">
      <p>
        {{ result }}
      </p>
      <button class="closeBtn" @click="showResult = false">X</button>
    </div>
  </div>
</template>

<script lang="ts">
import { ref, defineComponent, onMounted, watch } from "vue";
import GameGrid from "./components/GameGrid.vue";
import Keyboard from "./components/Keyboard.vue";

export default defineComponent({
  components: {
    GameGrid,
    Keyboard,
  },
  setup() {
    let grid = ref(["", "", "", "", "", ""]); // grille des mots entrés
    let gridStates = ref(["", "", "", "", "", ""]); // grille des états des lettres (valide, present, incorrect)
    watch(gridStates, () => {
      gridStates;
    });
    let currentRow = 0; // ligne en cours
    let word = ""; // mot à trouver
    let wordsList: Array<string> = [
      "loupe",
      "aigle",
      "chien",
      "boite",
      "flute",
    ]; // dictionnaire
    let result = ref(""); // message de validation
    let showResult = ref(false);

    function addLetter(letter: string) {
      if (grid.value[currentRow].length < 5) {
        grid.value[currentRow] += letter;
      }
      console.log(grid.value[0]);
    }

    function getRandomInt(max: number) {
      return Math.floor(Math.random() * max);
    }

    function validateState() {
      const wordSent = grid.value[currentRow];

      for (let i = 0; i < wordSent.length; i++) {
        if (word.charAt(i) === wordSent.charAt(i)) {
          gridStates.value[currentRow] += "v"; // valid
        } else if (word.includes(wordSent[i])) {
          gridStates.value[currentRow] += "p"; // present
        } else {
          gridStates.value[currentRow] += "i"; // incorrect
        }
      }
      console.log("validation... " + wordSent);
      console.log(gridStates.value[currentRow]);
    }

    function validate() {
      const wordSent = grid.value[currentRow];

      if (wordSent.length != 5) {
        return;
      }

      if (wordSent === word && wordsList.includes(wordSent)) {
        // Bon mot.
        validateState();
        result.value = "GAGNÉ";
        showResult.value = true;
        console.log("GAGNÉ");
      } else if (wordsList.includes(wordSent)) {
        // Mot appartenant au dictionnaire

        validateState();
        console.log("Incorrect");
        currentRow++;
        if (currentRow == 6) {
          // mais limite d'essai atteinte
          console.log("perdu");
          result.value = "PERDU";
          showResult.value = true;
        }
      } else {
        // Mot n'appartenant pas au dictionnaire
        console.log("mot entré : " + wordSent);
        console.log("mot à trouver : " + word);
        result.value = "Ce mot n'est pas dans la liste.";
        showResult.value = true;
      }
    }

    function clear() {
      if (grid.value[currentRow].length > 0) {
        grid.value[currentRow] = grid.value[currentRow].slice(0, -1);
      }
    }

    onMounted(() => {
      word = wordsList[getRandomInt(wordsList.length - 1)];
    });

    return {
      grid,
      gridStates,
      result,
      showResult,

      addLetter,
      validate,
      clear,
    };
  },
});
</script>

<style lang="scss">
html {
  background-color: #121212;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  background-color: #121212;
}
h1 {
  color: lightgray;
  font-size: 2.5em;
  letter-spacing: 2px;
}
.result {
  position: absolute;
  top: 10%;
  left: 10%;
  height: 80%;
  width: 80%;
  font-size: 30px;
  border-radius: 40px;
  display: flex;
  justify-content: center;
  flex-direction: column;
  align-items: center;
  background-color: #212121;
  color: whitesmoke;
}
.closeBtn {
  color: gray;
  border: none;
  background-color: #121212;
  font-size: 1em;
  padding: 10px;
  border-radius: 10px;
}
</style>
