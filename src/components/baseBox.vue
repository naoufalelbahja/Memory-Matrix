<template>
  <div
    :class="{ box: true, active: active && checked, red: !active && checked }"
    @click="$emit('checkTile')"
  ></div>
</template>

<script>
export default {
  emits: ["checkTile"],
  props: {
    active: {
      type: Boolean,
      default: false,
    },
    checked: {
      type: Boolean,
      default: false,
    },
  },
};
</script>

<style scoped>
.box {
  flex-basis: 70px;
  width: 70px;
  margin-right: 8px;
  background-color: rgba(255, 255, 255, 0.05);
  border-radius: 5px;
}
.box.active {
  background-color: #748da5;
}
.box.red {
  background-color: rgb(187, 119, 119);
}
.box:last-child {
  margin-right: 0;
}
</style>
