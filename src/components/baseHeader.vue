<template>
  <header>
    <h1>Memory Matrix</h1>
    <h1>
      level <strong>{{ level }}</strong>
    </h1>
  </header>
</template>

<script>
export default {
  props: ["level"],
};
</script>

<style scoped>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-basis: 70px;
  background-color: rgba(0, 0, 0, 0.2);
  padding: 0 20px;
}
</style>
