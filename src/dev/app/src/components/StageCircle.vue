<template>
  <div
    class="timeline__stage-circle"
    :class="{
      completed: stage.isCompleted,
      current: currentStage == stage.id,
    }"
  >
    <img class="stage-circle__icon" :src="stage.icon" alt="stage icon" />
  </div>
</template>

<script>
export default {
  name: "StageCircle",
  props: ["stage", "currentStage"],
};
</script>

<style scoped>
.timeline__stage-circle {
  padding: 12px;
  display: inline-block;
  z-index: 2;
  border: 4px solid var(--gray);
  border-radius: 1000px;
  filter: saturate(0%);
  background: var(--light-gray);
}
.timeline__stage-circle:first-child {
  margin-right: 30px;
}
.timeline__stage-circle:nth-child(11) {
  border-radius: 15px;
  margin-left: 30px;
}
.stage-circle__icon {
  width: 45px;
  display: block;
}

.timeline__stage-circle.completed {
  filter: saturate(100%);
  border-color: var(--light-green);
  background: var(--pale-light-green);
}
.timeline__stage-circle.current {
  border-width: 6px;
}
</style>
