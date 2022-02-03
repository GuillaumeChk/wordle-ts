<template>
  <div
    class="tile"
    :class="{ present: isPresent, valid: isValid, incorrect: isIncorrect }"
  >
    {{ letter }}
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  props: {
    letter: String,
    letterState: {
      type: String,
      required: true,
    },
  },

  setup(props) {
    let isPresent = false;
    let isValid = false;
    let isIncorrect = false;

    if (props.letterState === "v") {
      isValid = true;
    } else if (props.letterState === "p") {
      isPresent = true;
    } else if (props.letterState === "i") {
      isIncorrect = true;
    }

    return {
      isPresent,
      isValid,
      isIncorrect,
    };
  },
});
</script>

<style lang="scss" scoped>
.tile {
  width: 60px;
  height: 65px;
  border: 2px solid #424242;
  margin: 3px;
  display: flex;
  justify-content: center;
  align-items: center;
  text-transform: capitalize;
  font-weight: bold;
  font-size: 30px;
  color: lightgray;
}
.present {
  background-color: orange;
  color: black;
}
.valid {
  background-color: forestgreen;
  color: black;
}
.incorrect {
  background-color: gray;
  color: black;
}
</style>
