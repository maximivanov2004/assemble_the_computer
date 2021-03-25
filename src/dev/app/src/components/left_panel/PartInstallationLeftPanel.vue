<template>
  <div class="left-panel__part-installation-left-panel">
    <div class="wrapper">
      <img
        v-for="part in parts"
        :src="part.part_image"
        alt="img"
        :key="part.part_name"
        :style="{
          width: part.image_width,
          height: part.image_height,
          top: part.image_top,
          left: part.image_left,
        }"
      />
      <button
        id="install-part-button"
        @click="installPart(step.part_name)"
        :class="{
          hide: installedParts[installedParts.length - 1] === step.part_name,
        }"
        :style="{
          width: currentPart.image_width,
          height: currentPart.image_height,
          top: currentPart.image_top,
          left: currentPart.image_left,
        }"
      ></button>
    </div>
  </div>
</template>

<script>
import parts from "../../data/parts.json";

export default {
  name: "PartInstallationLeftPanel",
  props: ["installedParts", "build", "step"],
  computed: {
    parts() {
      return this.installedParts.map((part_name) => {
        return parts[part_name].find(
          (part) => part.id === this.build[part_name]
        );
      });
    },
    currentPart() {
      return parts[this.step.part_name].find(
        (part) => part.id === this.build[this.step.part_name]
      );
    },
  },
  methods: {
    installPart(partName) {
      this.$emit("installPart", partName);
    },
  },
  mounted() {
    if (
      this.installedParts[this.installedParts.length - 1] ===
      this.step.part_name
    ) {
      return;
    }
    this.$emit("resetPartInstalled");
  },
  beforeupdate() {
    console.log("beforeupdate");
    this.$emit("resetPartInstalled");
  },
};
</script>

<style scoped>
.left-panel__part-installation-left-panel {
  flex: 1;
  display: flex;
  justify-content: center;
  align-items: center;
}

.wrapper {
  width: 500px;
  height: 500px;
  position: relative;
}

img {
  position: absolute;
  z-index: 0;
}

#install-part-button {
  position: absolute;
  z-index: 1;
  border: 4px solid var(--dark-gray);
  border-radius: 15px;
  background: rgba(255, 255, 255, 0.5);
}
#install-part-button:hover {
  border-color: var(--main-green);
}

#install-part-button.hide {
  display: none;
}
</style>
