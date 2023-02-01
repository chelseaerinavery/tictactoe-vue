<template>
  <div id="app">
    <div id="header">Tic-Tac-Toe</div>
    <TheGame />
  </div>
</template>

<script>
import TheGame from "./components/TheGame.vue";
export default {
  name: "App",
  components: {
    TheGame,
  },
};
</script>

<style scoped>
#app {
  display: flex;
  flex-direction: column;
  align-items: center;
}

#header {
  font-family: rubik-puddles;
  font-size: 2.5em;
  color: #de00cf;
}
</style>
