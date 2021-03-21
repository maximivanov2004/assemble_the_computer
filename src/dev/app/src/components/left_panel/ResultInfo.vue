<template>
  <div class="left-panel__result-info">
    <div v-for="(partId, partName, index) in build" :key="index">
      partName: "{{ partName }}" partScore: {{ partScore(partName, partId) }}
    </div>
  </div>
</template>

<script>
import parts from "../../data/parts.json";
import tasks from "../../data/tasks.json";

export default {
  name: "ResultInfo",
  props: ["build", "activeTask"],
  data() {
    return {
      scores: [],
    };
  },
  methods: {
    partScore(partName, partId) {
      const task = tasks.find((task) => task.id === this.activeTask);
      const part = parts[partName].find((part) => part.id === partId);

      if (part.group !== task.parts_group) {
        this.scores.push(0);
        return 0;
      } else {
        this.scores.push(1);
        return 1;
      }
    },
  },
  mounted() {
    console.log("resultMounted");
    this.$emit("resultMounted", this.scores);
  },
};
</script>
