<template>
  <div class="part-info">
    <div
      class="part-info__item"
      v-for="(charName, charValue) in part.characteristics"
      :key="charName"
    >
      {{ charName }} : {{ charValue }}
    </div>
  </div>
</template>

<script>
import parts from "../../data/parts.json";

export default {
  name: "PartInfo",
  props: ["build", "step"],
  computed: {
    part() {
      return parts[this.step.part_name].find(
        (part) => part.id === this.build[this.step.part_name]
      );
    },
  },
};
</script>

<style scoped>
.part-info__item {
  font-size: 22px;
  font-weight: 300;
}
</style>
