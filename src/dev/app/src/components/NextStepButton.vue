<template>
  <div
    class="main-panel__next-step-button"
    :class="{ disabled: currentStage !== activeStage || !partInstalled }"
    @click="nextStep"
  >
    <span v-if="currentStage === 0">Начать</span>
    <span v-else-if="currentStage < 10">Далее</span>
    <span v-else>Завершить</span>

    <img
      v-if="currentStage < 10"
      class="next-step-button__icon"
      src="../assets/icons/next_step_arrow.png"
      alt="next step icon"
    />
    <img
      v-else
      class="next-step-button__icon"
      src="../assets/icons/white_check_mark.png"
      alt="next step icon"
    />
  </div>
</template>

<script>
export default {
  name: "NextStepButton",
  props: ["activeStage", "currentStage", "partInstalled"],
  methods: {
    nextStep() {
      this.$emit("nextStep");
    },
  },
};
</script>

<style scoped>
.main-panel__next-step-button {
  position: absolute;
  bottom: -4px;
  left: -4px;
  right: -4px;
  padding: 20px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  font-size: 50px;
  color: white;
  border: 4px solid var(--dark-green);
  border-radius: 0 0 30px 0;
  background: var(--main-green);
}
.main-panel__next-step-button.disabled {
  border-color: #aaa;
  background: #bbb;
}
.next-step-button__icon {
  width: 65px;
}
</style>
