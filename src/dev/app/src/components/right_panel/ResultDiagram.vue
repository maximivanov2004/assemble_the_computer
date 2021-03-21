<template>
  <div class="result-diagram">result: {{ percent }}%</div>
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
