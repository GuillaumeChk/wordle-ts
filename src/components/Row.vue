<template>
  <div class="row">
    <Tile
      v-for="index in 5"
      :letter="word.charAt(index - 1)"
      :key="index - 1"
    />

    <!-- <Tile id="0" :letter="word.charAt(0)" />
    <Tile id="1" :letter="word.charAt(1)" />
    <Tile id="2" :letter="word.charAt(2)" />
    <Tile id="3" :letter="word.charAt(3)" />
    <Tile id="4" :letter="word.charAt(4)" /> -->
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
