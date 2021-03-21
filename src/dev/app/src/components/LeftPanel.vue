<template>
  <div class="main-panel__left-panel">
    <div class="left-panel__title">{{ step.left_title }}</div>
    <TasksList
      v-if="step.type === 'task_selection'"
      :activeTask="activeTask"
      @changeActiveTask="changeActiveTask"
    />
    <PartsList
      v-if="step.type === 'part_selection'"
      :step="step"
      :build="build"
      @selectPart="selectPart"
    />
    <PartInstallationLeftPanel
      v-if="step.type === 'part_installation'"
      :installedParts="installedParts"
      :build="build"
      :step="step"
      @installPart="installPart"
      @resetPartInstalled="resetPartInstalled"
    />
    <ResultInfo
      v-if="step.type === 'result'"
      :build="build"
      :activeTask="activeTask"
      @resultMounted="resultMounted"
    />
  </div>
</template>

<script>
import TasksList from "./left_panel/TasksList.vue";
import PartsList from "./left_panel/PartsList.vue";
import PartInstallationLeftPanel from "./left_panel/PartInstallationLeftPanel.vue";
import ResultInfo from "./left_panel/ResultInfo.vue";

export default {
  name: "LeftPanel",
  components: {
    TasksList,
    PartsList,
    PartInstallationLeftPanel,
    ResultInfo,
  },
  props: ["activeTask", "step", "build", "installedParts"],
  methods: {
    changeActiveTask(taskId) {
      this.$emit("changeActiveTask", taskId);
    },
    selectPart(partName, partId) {
      this.$emit("selectPart", partName, partId);
    },
    resultMounted(scores) {
      this.$emit("resultMounted", scores);
    },
    installPart(partName) {
      this.$emit("installPart", partName);
    },
    resetPartInstalled() {
      this.$emit("resetPartInstalled");
    },
  },
};
</script>

<style scoped>
.main-panel__left-panel {
  display: flex;
  flex-direction: column;
}

.left-panel__title {
  padding: 30px;
  font-size: 35px;
  font-weight: 500;
  border-bottom: 4px solid var(--gray);
}
</style>
