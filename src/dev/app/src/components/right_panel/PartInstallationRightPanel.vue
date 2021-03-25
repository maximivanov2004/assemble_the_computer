<template>
  <div class="part-installation-right-panel">
    <p>Нажмите в нужное место</p>
    <div
      class="part-image"
      :style="{ backgroundImage: `url(${imgSource})` }"
    ></div>
  </div>
</template>

<script>
import parts from "../../data/parts.json";

export default {
  name: "PartInstallationRightPanel",
  props: ["build", "step"],
  computed: {
    imgSource() {
      return parts[this.step.part_name].find(
        (part) => part.id === this.build[this.step.part_name]
      ).part_image;
    },
  },
};
</script>

<style scoped>
.part-image {
  width: 200px;
  height: 200px;
  background-size: contain;
  background-repeat: no-repeat;
}
</style>
