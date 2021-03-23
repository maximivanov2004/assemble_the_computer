<template>
  <div class="timeline-wrapper">
    <div class="timeline__restart-button" @click="restart">
      <img
        class="restart-button__icon"
        src="../assets/icons/restart.png"
        alt="restart icon"
      />
    </div>
    <div class="timeline">
      <StageCircle
        v-for="stage in stages"
        :key="stage.id"
        :stage="stage"
        :currentStage="currentStage"
        @click="changeCurrentStage(stage.id)"
      />
      <div class="timeline__line timeline__line-green"></div>
      <div class="timeline__line timeline__line-gray"></div>
    </div>
  </div>
</template>

<script>
import StageCircle from "./StageCircle.vue";
import stages from "../data/stages.json";

export default {
  name: "Timeline",
  components: {
    StageCircle,
  },
  props: ["activeStage", "currentStage"],
  computed: {
    stages() {
      return stages.map((stage) => {
        return {
          ...stage,
          isCompleted: stage.id <= this.activeStage,
        };
      });
    },
  },
  methods: {
    restart() {
      this.$emit("restart");
    },
    changeCurrentStage(stageId) {
      if (stageId <= this.activeStage) {
        this.$emit("changeCurrentStage", stageId);
      }
    },
  },
};
</script>

<style scoped>
.timeline-wrapper {
  margin: 30px 30px 0 30px;
  margin-bottom: 30px;
  display: flex;
  align-items: center;
}

.timeline__restart-button {
  margin-right: 25px;
  padding: 8px;
  border: 4px solid var(--red);
  border-radius: 1000px;
  background: #fee3e3;
}
.restart-button__icon {
  width: 38px;
  display: block;
}

.timeline {
  position: relative;
  flex: 1;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.timeline__line {
  height: 4px;
  position: absolute;
  top: 50%;
  transform: translate(0, -50%);
}
.timeline__line-green {
  z-index: 1;
  background: var(--main-green);
}
.timeline__line-gray {
  width: 100%;
  background: var(--dark-gray);
}
</style>
