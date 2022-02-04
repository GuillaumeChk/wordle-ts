<template>
  <div
    class="tile"
    :class="{
      present: letterState === 'p',
      valid: letterState === 'v',
      incorrect: letterState === 'i',
    }"
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
