<template>
  <div class="parts-list">
    <div
      class="parts-list__part-item"
      :class="{
        active: part.id === build[step.part_name],
      }"
      v-for="part in parts"
      :key="part.id"
      @click="selectPart(part.id)"
    >
      <div
        class="img"
        :style="{ backgroundImage: `url('${part.image}')` }"
      ></div>
      <!-- <img class="part-item__image" :src="part.image" alt="part image" /> -->
      <span class="part-item__name">{{ part.name }}</span>
    </div>
  </div>
</template>

<script>
import parts from "../../data/parts.json";

export default {
  name: "PartsList",
  props: ["step", "build"],
  computed: {
    parts() {
      return parts[this.step.part_name];
    },
  },
  methods: {
    selectPart(partId) {
      this.$emit("selectPart", this.step.part_name, partId);
    },
  },
  beforeCreate() {
    if (this.build[this.step.part_name] === null) {
      this.$emit("selectPart", this.step.part_name, 0);
    }
  },
  beforeUpdate() {
    if (this.build[this.step.part_name] === null) {
      this.$emit("selectPart", this.step.part_name, 0);
    }
  },
};
</script>

<style scoped>
.parts-list {
  padding-bottom: 10px;
  overflow-y: auto;
  overflow-x: hidden;
  flex: 1;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

.parts-list__part-item {
  padding: 12px 30px 50px 30px;
  margin: 10px 20px 0 20px;
  width: 240px;
  height: 240px;
  position: relative;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
  border: 4px solid var(--dark-gray);
  border-radius: 20px;
  background: var(--gray);
}

.img {
  width: 100%;
  height: 100%;
  background-size: contain;
  background-repeat: no-repeat;
  background-position: center;
}

/* .part-item__image {
  margin: 15px 0;
  height: 70%;
  display: block;
} */

.part-item__name {
  padding: 5px 0;
  position: absolute;
  bottom: -4px;
  left: -4px;
  right: -4px;
  text-align: center;
  font-size: 18px;
  border: 4px solid #ddd;
  border-radius: 0 0 20px 20px;
  background: var(--dark-gray);
}

.parts-list__part-item.active {
  border-color: var(--light-green);
  background: var(--pale-light-green);
}
.parts-list__part-item.active .part-item__name {
  border-color: var(--main-green);
  background: var(--light-green);
}
</style>
