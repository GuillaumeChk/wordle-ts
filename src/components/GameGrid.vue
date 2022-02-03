<template>
  <div class="gameGrid">
    <Row
      v-for="(word, index) in grid"
      :word="word"
      :key="index"
      :word-state="gridStates[index]"
    />
  </div>
</template>

<script lang="ts">
import { defineComponent, PropType } from "vue";
import Row from "./Row.vue";

export default defineComponent({
  props: {
    grid: {
      type: Array as PropType<string[]>,
      required: true,
    },
    gridStates: {
      type: Array as PropType<string[]>,
      required: true,
    },
  },
  components: {
    Row,
  },
});
</script>

<style lang="scss" scoped>
.gameGrid {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
