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
  border-bottom: 2px solid #ccc;
  display: flex;
  font-size: 22px;
  font-weight: 300;
}
.part-info__item span {
  padding: 0 10px;
}
.part-info__item:first-child {
  border-top: 2px solid #ccc;
}
.part-info__item span:last-child {
  background: #eee;
}

.part-info__item:nth-child(2n) {
  background: var(--gray);
}
.part-info__item:nth-child(2n) span:last-child {
  padding-left: 10px;
  background: #dedede;
}

.part-info__item span:last-child {
  margin-left: auto;
}
</style>
