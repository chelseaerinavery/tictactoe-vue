<template>
  <div class="board">
    <div class="board-edge clearfix">
      <div class="board-boundary">
        <div class="board-body">
          <div class="board-row">
            <square :content="squares[0]" @click="OnClicked(0)" />
            <square :content="squares[1]" @click="OnClicked(1)" />
            <square :content="squares[2]" @click="OnClicked(2)" />
          </div>
          <div class="board-row">
            <square :content="squares[3]" @click="OnClicked(3)" />
            <square :content="squares[4]" @click="OnClicked(4)" />
            <square :content="squares[5]" @click="OnClicked(5)" />
          </div>
          <div class="board-row">
            <square :content="squares[6]" @click="OnClicked(6)" />
            <square :content="squares[7]" @click="OnClicked(7)" />
            <square :content="squares[8]" @click="OnClicked(8)" />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Square from "./TheSquare.vue";
export default {
  name: "TheBoard",
  props: {
    squares: Array,
    OnHandleClick: Function,
  },
  components: {
    Square,
  },
  methods: {
    OnClicked(i) {
      this.OnHandleClick(i);
    },
  },
};
</script>

<style scoped>
.board-row {
  clear: both;
  display: table;
}
.board-boundary {
  position: relative;
  float: left;
  left: 50%;
}
.board-body {
  position: relative;
  left: -50%;
}
.clearfix::after {
  content: "";
  display: block;
  height: 0;
  clear: both;
  visibility: hidden;
}
</style>
