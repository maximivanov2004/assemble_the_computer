<template>
  <div class="wrapper">
    <ul class="left-panel__tasks-list">
      <li
        class="tasks-list__task"
        v-for="(task, index) in tasks"
        :key="task.id"
        :class="{ active: task.id === activeTask }"
        @click="changeActiveTask(task.id)"
      >
        {{ index + 1 }}. {{ task.title }}
      </li>
    </ul>
  </div>
</template>

<script>
import tasks from "../../data/tasks.json";

export default {
  name: "TasksList",
  props: ["activeTask"],
  data() {
    return { tasks };
  },
  methods: {
    changeActiveTask(taskId) {
      this.$emit("changeActiveTask", taskId);
    },
  },
};
</script>

<style scoped>
.wrapper {
  flex: 1;
  /* overflow-y: auto;
  overflow-x: hidden; */
}
.left-panel__tasks-list {
  margin: 0;
  padding: 0;
}

.tasks-list__task {
  padding: 30px;
  position: relative;
  display: block;
  list-style-type: none;
  font-size: 30px;
  border-bottom: 4px solid var(--gray);
}
.tasks-list__task.active {
  color: white;
  background: var(--main-green);
}
.tasks-list__task.active::before {
  content: "";
  position: absolute;
  top: -4px;
  left: -4px;
  width: 100%;
  height: 100%;
  display: block;
  z-index: 3;
  box-sizing: content-box;
  border: 4px solid var(--dark-green);
}
</style>
