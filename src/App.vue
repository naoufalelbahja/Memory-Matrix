<template>
  <section class="main_container">
    <base-header :level="level"></base-header>
    <base-board
      :playing="playing"
      :nTiles="nTiles"
      :checkedTiles="checkedTiles"
      :board="board"
      @checkTile="checkTile"
    ></base-board>
    <base-message
      v-if="message !== null"
      :title="message?.title"
      :message="message?.message"
    >
      <button type="button" @click="message?.btn[1](message?.btn[2])">
        {{ message?.btn[0] }}
      </button>
    </base-message>
  </section>
</template>

<script>
import baseHeader from "./components/baseHeader.vue";
import baseBoard from "./components/baseBoard.vue";
import baseMessage from "./components/baseMessage.vue";
export default {
  components: { baseHeader, baseBoard, baseMessage },
  data() {
    return {
      playing: false,
      board: [],
      level: 1,
      nTiles: 6,
      checkedTiles: [],
      message: null,
    };
  },
  methods: {
    startGame(won) {
      this.playing = false;
      setTimeout(() => (this.playing = true), 1000);
      this.message = null;
      this.checkedTiles = [];
      this.board = [];
      this.generateBoard(won);
    },
    generateBoard(won) {
      this.nTiles += won ? Math.floor(Math.random() * 3) + 1 : 0;
      this.level += won ? 1 : 0;
      let i;
      for (i = this.nTiles * 2; i ** 0.5 % 1 !== 0; i++);
      i **= 0.5;

      for (let j = 0; j < i; j++) {
        const arr = [];
        for (let j = 0; j < i; j++) arr.push(false);
        this.board.push(arr);
      }

      let r = 1;
      while (r <= this.nTiles) {
        const rRow = Math.floor(Math.random() * i);
        const rCol = Math.floor(Math.random() * i);
        if (!this.board[rRow][rCol]) {
          this.board[rRow].splice(rCol, 1, true);
          r++;
        }
      }
    },
    checkTile(tileId) {
      if (!this.checkedTiles.includes(tileId) && this.playing) {
        this.checkedTiles.push(tileId);
        if (this.checkedTiles.length === this.nTiles) {
          this.displayResult();
        }
      }
    },
    displayResult() {
      this.playing = false;
      let incorrect = 0;
      for (let tile of this.checkedTiles) {
        const splt = tile.split("-").map((el) => Number(el));
        incorrect += !this.board[splt[0]][splt[1]] ? 1 : 0;
      }
      setTimeout(
        () => {
          this.message = {
            title: "The Game is Over",
            message:
              "You Have Ended the game by " +
              incorrect +
              " mistakes. do you want to pass to the next level?",
            btn: ["Next", this.startGame, incorrect === 0],
          };
        },
        incorrect === 0 ? 200 : 1000
      );
    },
  },
  mounted() {
    this.message = {
      title: "Memory Matrix",
      message:
        "tiles will apear ni different color. remember theire places and check them after they disappear.",
      btn: ["Start Game", this.startGame, false],
    };
  },
};
</script>

<style>
* {
  padding: 0;
  margin: 0;
  font-family: "Courier New", Courier, monospace;
  color: #eee;
  box-sizing: border-box;
}
html {
  font-size: 20px;
}
.main_container {
  display: flex;
  flex-direction: column;
  height: 100vh;
  width: 100vw;
  background-color: rgb(9, 95, 105);
}
</style>

<style>
h1,
h2,
h3,
h4 {
  text-transform: capitalize;
}
h1 {
  font-size: 150%;
}
button {
  border: none;
  background-color: #2c3e50;
  color: #eee;
  border-radius: 3px;
  padding: 15px 25px;
  font-size: 100%;
  transition: all 0.3s;
}
button:hover {
  background-color: #253544;
  color: #fff;
}
</style>
