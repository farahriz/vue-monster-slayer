<template>
  <div id="app">
    <div id="player" class="player-space">
      <img src="./assets/logo.png">
      <h2>Player</h2>
      <HealthBar :health="playerHealth"></HealthBar>
    </div>
    <div id="monster" class="player-space">
      <img src="./assets/logo.png">
      <h2>Monster</h2>
      <HealthBar :health="monsterHealth"></HealthBar>
    </div>
    <div id="controls">
      <Button></Button>
      <Button>Special Attack</Button>
      <Button>Heal</Button>
      <Button>Give Up</Button>
    </div>
    <ActionLog/>
  </div>
</template>

<script>
import HealthBar from "./components/HealthBar";
import Button from "./components/Button";
import ActionLog from "./components/ActionLog";

export default {
  name: "App",
  components: {
    HealthBar,
    Button,
    ActionLog
  },
  data() {
    return {
      monsterHealth: 100,
      playerHealth: 100
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  display: flex;
  flex-wrap: wrap;
}

#controls {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  display: flex;
  justify-content: space-between;
  height: 100%;
  margin: 0 auto;
}

.player-space {
  width: 50%;
}
</style>
