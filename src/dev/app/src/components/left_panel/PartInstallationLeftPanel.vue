<template>
  <div class="left-panel__part-installation-left-panel">
    <img
      v-for="imageSource in images"
      :src="imageSource"
      alt="img"
      :key="imageSource"
    />
    <button
      id="install-part-button"
      @click="installPart(step.part_name)"
      :class="{
        hide: installedParts[installedParts.length - 1] === step.part_name,
      }"
    >
      install {{ step.part_name }}
    </button>
  </div>
</template>

<script>
import parts from "../../data/parts.json";

export default {
  name: "PartInstallationLeftPanel",
  props: ["installedParts", "build", "step"],
  computed: {
    images() {
      return this.installedParts.map((part_name) => {
        return parts[part_name].find(
          (part) => part.id === this.build[part_name]
        ).part_image;
      });
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
  position: relative;
}

img {
  position: absolute;
  z-index: 0;
}

#install-part-button {
  position: absolute;
  z-index: 1;
}

#install-part-button.hide {
  display: none;
}
</style>
