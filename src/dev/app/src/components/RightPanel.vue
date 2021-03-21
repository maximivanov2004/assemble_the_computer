<template>
  <div class="main-panel__right-panel">
    <div class="right-panel__title">{{ rightTitle }}</div>

    <TaskDescription
      v-if="step.type === 'task_selection'"
      :activeTask="activeTask"
    />
    <PartInfo
      v-if="step.type === 'part_selection'"
      :build="build"
      :step="step"
    />
    <PartInstallationRightPanel
      v-if="step.type === 'part_installation'"
      :build="build"
      :step="step"
    />
    <ResultDiagram v-if="step.type === 'result'" :scores="scores" />
    <div v-if="step.type !== 'task_selection'" class="final-price">
      Итоговая стоимость: {{ finalPrice }} рублей
    </div>
  </div>
</template>

<script>
import TaskDescription from "./right_panel/TaskDescription.vue";
import PartInfo from "./right_panel/PartInfo.vue";
import PartInstallationRightPanel from "./right_panel/PartInstallationRightPanel.vue";
import ResultDiagram from "./right_panel/ResultDiagram.vue";
import parts from "../data/parts.json";

export default {
  name: "RightPanel",
  components: {
    TaskDescription,
    PartInfo,
    PartInstallationRightPanel,
    ResultDiagram,
  },
  props: ["activeTask", "step", "build", "scores"],
  computed: {
    finalPrice() {
      return Object.keys(this.build).reduce((finalPrice, key) => {
        if (this.build[key] !== null) {
          return (
            finalPrice +
            parts[key].find((part) => part.id === this.build[key]).price
          );
        }
        return finalPrice;
      }, 0);
    },
    rightTitle() {
      return this.step.type === "task_selection"
        ? "Описание:"
        : this.step.type === "part_selection"
        ? "Характеристики:"
        : this.step.type === "part_installation"
        ? parts[this.step.part_name].find(
            (part) => part.id === this.build[this.step.part_name]
          ).name + ":"
        : "Итог:";
    },
  },
};
</script>

<style scoped>
.main-panel__right-panel {
  height: 100%;
  display: flex;
  flex-direction: column;
  padding: 15px;
}

.right-panel__title {
  font-size: 40px;
  font-weight: 300;
  margin-bottom: 10px;
}

.final-price {
  margin-top: auto;
  margin-bottom: 100px;
}
</style>
