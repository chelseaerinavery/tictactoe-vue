<template>
  <div class="game-body">
    <div class="game-status">{{ gameStatus }}</div>
    <TheBoard :squares="squares" :OnHandleClick="OnClicked"></TheBoard>
    <button v-if="isResetEnabled" @click="reset()">New Game</button>
  </div>
</template>

<script>
import TheBoard from "./TheBoard.vue";
export default {
  name: "TheGame",
  components: {
    TheBoard,
  },
  data: function () {
    return {
      winner: null,
      isPlayerX: true,
      squares: Array(9).fill(""),
      history: [
        {
          squares: Array(9).fill(null),
        },
      ],
    };
  },
  computed: {
    gameStatus: function () {
      if (this.winner === "X" || this.winner === "O") {
        return "Winner is " + this.winner;
      }
      if (this.winner === null && !this.squares.includes("")) {
        return "DRAW";
      }
      if (this.isPlayerX) {
        return "Next Player: X";
      } else {
        return "Next Player: O";
      }
    },
    isResetEnabled: function () {
      if (this.winner === "X" || this.winner === "O") {
        return true;
      }
      for (let i = 0; i < this.squares.length; i++) {
        if (this.squares[i] != "X" && this.squares[i] != "O") {
          return false;
        }
      }
      return true;
    },
  },
  methods: {
    calculateWinner() {
      const lines = [
        [0, 1, 2],
        [3, 4, 5],
        [6, 7, 8],
        [0, 3, 6],
        [1, 4, 7],
        [2, 5, 8],
        [0, 4, 8],
        [2, 4, 6],
      ];
      for (let i = 0; i < lines.length; i++) {
        const [a, b, c] = lines[i];
        if (
          this.squares[a] &&
          this.squares[a] === this.squares[b] &&
          this.squares[b] === this.squares[c]
        ) {
          this.winner = this.squares[a];
          return;
        }
      }
    },
    OnClicked(i) {
      if (this.winner === "X" || this.winner === "O") {
        return;
      }
      if (this.squares[i] === "X" || this.squares[i] === "O") {
        return;
      }
      this.squares[i] = this.isPlayerX ? "X" : "O";
      this.isPlayerX = !this.isPlayerX;
      this.calculateWinner();
    },
    reset() {
      for (let i = 0; i < this.squares.length; i++) {
        this.squares[i] = "";
      }
      this.winner = null;
    },
  },
};
</script>
