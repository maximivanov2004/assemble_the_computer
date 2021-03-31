<template>
  <div class="left-panel__result-info">
    <div class="wrapper">
      <div
        v-for="(partId, partName, index) in build"
        :key="index"
        class="result-item"
        :class="{ wrong: partScore(partName, partId) === 0 }"
      >
        <img
          v-if="partScore(partName, partId) === 1"
          class="part-mark"
          src="../../assets/icons/green_check_mark.png"
          alt="check mark"
        />
        <img
          v-else
          class="part-mark"
          src="../../assets/icons/x_mark.png"
          alt="check mark"
        />
        <img class="part-icon" :src="partsIcons[partName]" alt="part icon" />
      </div>
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
      partsIcons: {
        processor: "./assets/icons/cpu.png",
        motherboard: "./assets/icons/motherboard.png",
        case: "./assets/icons/computer_case.png",
        cooling: "./assets/icons/cooling_fan.png",
        ram: "./assets/icons/ram_memory.png",
        video_card: "./assets/icons/video_card.png",
        hard_drive: "./assets/icons/harddisk.png",
        ssd: "./assets/icons/ssd.png",
        power_supply: "./assets/icons/power.png",
      },
    };
  },
  methods: {
    partScore(partName, partId) {
      const task = tasks.find((task) => task.id === this.activeTask);
      const part = parts[partName].find((part) => part.id === partId);

      if (task.parts_group === 0) return 1;

      if (part.group.includes(task.parts_group)) {
        return 1;
      } else {
        return 0;
      }
    },
  },
  mounted() {
    const scores = Object.keys(this.build).map((key) => {
      const partName = key;
      const partId = this.build[partName];

      const task = tasks.find((task) => task.id === this.activeTask);
      const part = parts[partName].find((part) => part.id === partId);

      console.log(task.parts_group, part.group);

      if (task.parts_group === 0) return 1;

      if (part.group.includes(task.parts_group)) {
        return 1;
      } else {
        return 0;
      }
    });

    this.$emit("resultMounted", scores);
  },
};
</script>

<style scoped>
.left-panel__result-info {
  flex: 1;
  display: flex;
  justify-content: center;
  align-items: center;
}

.wrapper {
  margin-bottom: -60px;
  max-width: 700px;
  display: flex;
  flex-wrap: wrap;
}

.result-item {
  margin-bottom: 60px;
  width: 33.3%;
  display: flex;
  justify-content: center;
  align-items: center;
}

.part-mark {
  width: 65px;
}

.part-icon {
  margin-left: 30px;
  padding: 10px;
  width: 90px;
  display: block;
  border: 4px solid var(--light-green);
  border-radius: 15px;
  background: var(--pale-light-green);
}

.result-item.wrong .part-icon {
  border-color: var(--red);
  background: var(--pale-red);
}

.result-item.wrong .part-mark {
  width: 55px;
}
</style>
