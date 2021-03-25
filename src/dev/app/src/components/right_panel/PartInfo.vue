<template>
  <div class="part-info">
    <div
      class="part-info__item"
      v-for="(charValue, charName) in part.characteristics"
      :key="charName"
    >
      <span>{{ charName }}: </span><span>{{ charValue }}</span>
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
.part-info {
  overflow: auto;
  height: 420px;
}

.part-info__item {
  display: flex;
  align-items: center;
  font-size: 22px;
  font-weight: 300;
}

.part-info__item:nth-child(2n) {
  background: var(--gray);
}

.part-info__item span:last-child {
  margin-left: auto;
}
</style>
