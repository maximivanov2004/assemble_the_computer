<template>
  <div class="result-diagram">
    <div
      class="percent"
      :class="{
        yellow: percent > 40 && percent < 70,
        red: percent < 40,
      }"
    >
      {{ percent }}%
    </div>
    <img
      class="diagram"
      :class="{
        yellow: percent > 40 && percent < 70,
        red: percent < 40,
      }"
      src="../../assets/icons/computer_case.png"
      alt="diagram"
    />
  </div>
</template>

<script>
export default {
  name: "ResultDiagram",
  props: ["scores"],
  computed: {
    percent() {
      return Math.round(
        (this.scores.reduce((acc, score) => acc + score, 0) / 9) * 100
      );
    },
  },
};
</script>

<style scoped>
.result-diagram {
  height: 420px;
  display: flex;
  align-items: center;
}

.percent {
  margin-left: 20px;
  font-size: 50px;
  color: var(--main-green);
}
.percent.yellow {
  color: var(--yellow);
}
.percent.red {
  color: var(--red);
}

.diagram {
  margin-left: auto;
  margin-right: 20px;
  padding: 40px;
  height: 270px;
  border: 14px solid var(--main-green);
  border-radius: 250px;
}
.diagram.yellow {
  border-color: var(--yellow);
}
.diagram.red {
  border-color: var(--red);
}
</style>
