<template>
  <section class="container">
    <h2>{{ nTiles - checkedTiles.length }} tiles are remaining</h2>

    <div class="board">
      <div class="row" v-for="(row, index) in board" :key="index">
        <base-box
          v-for="(box, index2) in row"
          :key="index + '-' + index2"
          :active="box"
          :checked="
            checkedTiles.includes(index + '-' + index2) || (!playing && box)
          "
          @checkTile="$emit('checkTile', index + '-' + index2)"
        ></base-box>
      </div>
    </div>
  </section>
</template>

<script>
import baseBox from "./baseBox.vue";
export default {
  emits: ["checkTile"],
  components: { baseBox },
  props: ["playing", "nTiles", "checkedTiles", "board"],
};
</script>

<style scoped>
.container {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  flex: 1;
}
.container h2 {
  margin: 20px;
}
.container .board {
  background-color: rgba(0, 0, 0, 0.3);
  border-radius: 7px;
  display: flex;
  flex-direction: column;
  padding: 13px;
}
.container .board .row {
  display: flex;
  flex-basis: 70px;
  margin-bottom: 8px;
  flex-direction: row;
}
.container .board .row:last-child {
  margin-bottom: 0;
}
</style>
