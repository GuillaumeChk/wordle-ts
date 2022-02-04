<template>
  <div class="row">
    <Tile
      v-for="index in 5"
      :letter="word.charAt(index - 1)"
      :key="index - 1"
      :letter-state="wordState.charAt(index - 1)"
    />
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import Tile from "./Tile.vue";

export default defineComponent({
  props: {
    word: {
      type: String,
      required: true,
    },
    wordState: {
      type: String,
      required: true,
    },
  },
  components: {
    Tile,
  },
});
</script>

<style lang="scss" scoped>
.row {
  display: inline-flex;
}
</style>
