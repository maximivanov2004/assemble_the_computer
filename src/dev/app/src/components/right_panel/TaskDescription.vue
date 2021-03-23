<template>
  <div class="right-panel__task-description">
    <p class="task-description__text">{{ task.description }}</p>
  </div>
</template>

<script>
import tasks from "../../data/tasks.json";

export default {
  name: "TaskDescription",
  props: ["activeTask"],
  computed: {
    task() {
      return tasks[this.activeTask];
    },
  },
};
</script>

<style scoped>
.right-panel__task-description {
  font-size: 35px;
  font-weight: 500;
}

.task-description__title,
.task-description__text {
  margin: 0;
  font-weight: 300;
}

.task-description__title {
  margin-bottom: 6px;
}

.task-description__text {
  overflow: auto;
  height: 445px;
  font-size: 32px;
}
</style>
