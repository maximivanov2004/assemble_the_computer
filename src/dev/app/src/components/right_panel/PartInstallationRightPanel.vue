<template>
  <div class="part-installation-right-panel">
    <p>Нажмите в нужное место</p>
    <img :src="imgSource" alt="image" height="100" width="100" />
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
