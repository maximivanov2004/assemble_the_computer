<template>
  <div class="main-panel">
    <LeftPanel
      :activeTask="activeTask"
      :step="steps[currentStep]"
      :build="build"
      :installedParts="installedParts"
      @changeActiveTask="changeActiveTask"
      @selectPart="selectPart"
      @resultMounted="setScores"
      @installPart="installPart"
      @resetPartInstalled="partInstalled = false"
    />
    <div class="main-panel__right-panel-wrapper">
      <RightPanel
        :activeTask="activeTask"
        :step="steps[currentStep]"
        :build="build"
        :scores="scores"
      />
      <NextStepButton
        :activeStage="activeStage"
        :currentStage="currentStage"
        :partInstalled="partInstalled"
        @nextStep="nextStep"
      />
    </div>
  </div>
</template>

<script>
import LeftPanel from "./LeftPanel.vue";
import RightPanel from "./RightPanel.vue";
import NextStepButton from "./NextStepButton.vue";

import stages from "../data/stages.json";
import parts from "../data/parts.json";

export default {
  name: "MainPanel",
  components: {
    LeftPanel,
    RightPanel,
    NextStepButton,
  },
  props: ["activeStage", "currentStage"],
  data() {
    return {
      activeTask: 0,
      activeStep: 0,
      currentStep: 0,
      scores: [],
      build: {
        processor: null,
        motherboard: null,
        case: null,
        cooling: null,
        ram: null,
        video_card: null,
        hard_drive: null,
        ssd: null,
        power_supply: null,
      },
      installedParts: ["case"],
      partInstalled: true,
    };
  },
  computed: {
    steps() {
      return stages[this.currentStage].steps;
    },
  },
  methods: {
    nextStep() {
      if (this.currentStage !== this.activeStage) return;
      // ------------------------
      const isPartValid = (partName, partId, build) => {
        const validatingPart = parts[partName].find(
          (part) => part.id === partId
        );

        if (!validatingPart.validation) return true;

        for (let partName in validatingPart.validation) {
          const checkingPart = parts[partName].find(
            (part) => part.id === build[partName]
          );

          for (let charName in validatingPart.validation[partName]) {
            if (
              !validatingPart.validation[partName][charName].includes(
                checkingPart.characteristics[charName]
              )
            ) {
              return false;
            }
          }
        }

        return true;
      };

      if (this.currentStage > 0 && this.currentStage < 10) {
        const step = this.steps.find((step) => step.id === this.activeStep);

        if (
          !isPartValid(step.part_name, this.build[step.part_name], this.build)
        ) {
          alert(
            "Ошибка совместимости! Проверьте характеристики детали и выберите другую из списка."
          );
          return;
        }
      }
      // ---------------------------
      if (!this.partInstalled) return;

      if (
        this.steps.find((step) => step.id === this.activeStep).type ===
        "part_installation"
      ) {
        this.partInstalled = false;
      }

      if (
        (this.build.video_card === 0 &&
          this.steps.find((step) => step.id === this.activeStep).part_name ===
            "video_card") ||
        (this.build.ssd === 0 &&
          this.steps.find((step) => step.id === this.activeStep).part_name ===
            "ssd")
      ) {
        this.activeStep = 0;
        this.currentStep = 0;
        this.partInstalled = true;
        this.$emit("nextStage");
        return;
      }

      if (this.activeStage === 10) {
        this.activeStep = 0;
        this.currentStep = 0;
        this.activeTask = 0;
        this.installedParts = ["case"];
        this.$emit("complete");
      } else if (this.currentStep === this.steps[this.steps.length - 1].id) {
        this.activeStep = 0;
        this.currentStep = 0;
        this.partInstalled = true;
        this.$emit("nextStage");
      } else {
        this.activeStep += 1;
        this.currentStep = this.activeStep;
      }
    },
    changeActiveTask(taskId) {
      if (this.activeStage === 0) {
        this.activeTask = taskId;
      }
    },
    selectPart(partName, partId) {
      if (this.currentStage === this.activeStage) {
        this.build[partName] = partId;
      }
    },
    setScores(scores) {
      this.scores = scores;
    },
    installPart(partName) {
      this.partInstalled = true;
      this.installedParts.push(partName);
    },
  },
};
</script>

<style scoped>
.main-panel {
  display: flex;
  border: 4px solid var(--gray);
  border-radius: 30px;
  background: var(--light-gray);
}

.main-panel__left-panel {
  flex: 2;
  height: 630px;
}

.main-panel__right-panel-wrapper {
  position: relative;
  width: 485px;
  border-left: 4px solid var(--gray);
}
</style>
