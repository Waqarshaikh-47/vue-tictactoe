<template>
  <div class="container d-flex justify-content-center">
    <div>
      <h2 v-if="winner" class="winner">Winner : {{ winner }} 🥳</h2>
      <h2 v-else class="player">Players {{ player }}</h2>
      <button @click="reset" class="btn btn-clr mb-3">Reset</button>
      <div v-for="x in 3" :key="x" class="row">
        <button
          v-for="y in 3"
          :key="y"
          class="square"
          @click="move(x - 1, y - 1)"
        >
          {{ squares[x - 1][y - 1] }}
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, computed } from "vue";

const calculateWinner = (squares) => {
  const lines = [
    [0, 1, 2],
    [3, 4, 5],
    [7, 8, 9],
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    [0, 4, 8],
    [2, 4, 6],
  ];
  for (let i = 0; i < lines.length; i++) {
    const [a, b, c] = lines[i];
    // console.log(
    // squares[a] && squares[a] === squares[b] && squares[a] === squares[c]
    // );
    if (squares[a] && squares[a] === squares[b] && squares[a] === squares[c]) {
      // console.log(squares[a]);
      return squares[a];
    }
  }
  return null;
};

export default {
  name: "BoardA",
  setup() {
    const player = ref("X");
    const squares = ref([
      ["", "", ""],
      ["", "", ""],
      ["", "", ""],
    ]);
    const winner = computed(() => calculateWinner(squares.value.flat()));
    // console.log(squares.value.flat());
    const move = (x, y) => {
      // console.log(winner.value);
      if (winner.value) {
        return;
      }
      squares.value[x][y] = player.value;
      player.value = player.value === "Y" ? "X" : "Y";
    };

    const reset = () => {
      player.value = "X";
      squares.value = [
        ["", "", ""],
        ["", "", ""],
        ["", "", ""],
      ];
    };

    return { player, squares, winner, move, reset };
  },
  props: {},
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.square {
  background: rgba(22, 85, 124, 0.582);
  border: 1px solid rgba(128, 0, 53, 0.995);
  float: left;
  font-size: 70px;
  font-weight: bold;
  line-height: 34px;
  height: 100px;
  margin-right: -1px;
  margin-top: -1px;
  padding: 0;
  text-align: center;
  width: 100px;
  color: rgba(128, 0, 53, 0.557);
}
.winner {
  color: rgba(128, 0, 53, 0.995);
  text-align: center;
}
.player {
  color: rgba(128, 0, 53, 0.995);
}
.btn-clr {
  color: rgba(128, 0, 53, 0.995);
  border-color: rgba(128, 0, 53, 0.557);
  background: rgba(22, 85, 124, 0.582);
}
</style>
