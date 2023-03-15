<template>
  <BoardA />
</template>

<script>
import BoardA from "./components/Board.vue";

export default {
  name: "App",
  components: {
    BoardA,
  },
};
</script>

<style>
body {
  background-color: rgba(34, 148, 218, 0.454);
}
</style>
