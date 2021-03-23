<template>
  <div class="header">
    <img class="header__logo" src="./assets/images/logo.png" alt="logo" />
    <span class="header__text">Build a computer - Собери компьютер</span>
  </div>
  <Timeline
    :activeStage="activeStage"
    :currentStage="currentStage"
    @restart="restart"
    @changeCurrentStage="changeCurrentStage"
  />
  <MainPanel
    ref="mainPanel"
    :activeStage="activeStage"
    :currentStage="currentStage"
    @complete="restart"
    @nextStage="nextStage"
  />
</template>

<script>
import Timeline from "./components/Timeline.vue";
import MainPanel from "./components/MainPanel.vue";

export default {
  name: "App",
  components: {
    Timeline,
    MainPanel,
  },
  data() {
    return {
      activeStage: 0,
      currentStage: 0,
    };
  },
  methods: {
    restart() {
      this.activeStage = 0;
      this.currentStage = 0;
      this.$refs.mainPanel.activeStep = 0;
      this.$refs.mainPanel.activeTask = 0;
      this.$refs.mainPanel.activeStep = 0;
      this.$refs.mainPanel.currentStep = 0;
      this.$refs.mainPanel.scores = [];
      this.$refs.mainPanel.build = {
        processor: null,
        motherboard: null,
        case: null,
        cooling: null,
        ram: null,
        video_card: null,
        hard_drive: null,
        ssd: null,
        power_supply: null,
      };
      this.$refs.mainPanel.installedParts = ["case"];
      this.$refs.mainPanel.partInstalled = true;
    },
    changeCurrentStage(stageId) {
      this.currentStage = stageId;

      if (this.currentStage === this.activeStage) {
        this.$refs.mainPanel.currentStep = this.$refs.mainPanel.activeStep;
      } else {
        this.$refs.mainPanel.currentStep = 0;
      }
    },
    nextStage() {
      this.activeStage += 1;
      this.currentStage = this.activeStage;
    },
  },
};
</script>

<style>
* {
  box-sizing: border-box;
}

html,
body,
#app {
  margin: 0;
  padding: 0;
  min-width: 1200px;
  height: 100%;
  font-family: Rubik;
}

:root {
  --main-green: #94d637;
  --light-green: #a9f340;
  --pale-light-green: #e8f7d2;
  --dark-green: #85bf34;

  --red: #ec2525;
  --pale-red: #fee3e3;

  --yellow: #efe543;
  --light-yellow: #f5eb52;
  --pale-light-yellow: #f7f4d2;

  --light-gray: #f7f7f7;
  --gray: #ededed;
  --dark-gray: #e9e9e9;
  --very-dark-gray: #333333;
}

body {
  height: 100vh;
}

#app {
  display: flex;
  flex-direction: column;
}

.header {
  height: 90px;
  display: flex;
  align-items: stretch;
  color: white;
  background: var(--main-green);
}
.header__logo {
  margin: 6px;
}
.header__text {
  font-family: "Roboto mono";
  font-size: 35px;
  margin-top: auto;
}

.main-panel {
  margin: 0 30px 30px 30px;
  flex: 1;
}
</style>
