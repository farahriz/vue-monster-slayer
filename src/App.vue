<template>
  <div id="app">
    <div class="container">
      <div class="row">
        <div class="col-lg-5">
          <h3>Player</h3>
        </div>
        <div class="col-lg-1">
          <h5>VS</h5>
        </div>
        <div class="col-lg-5">
          <h3>Monster</h3>
        </div>
      </div>
    </div>

    <div id="controls" class="container">
      <b-button size="lg" variant="primary">ATK</b-button>
      <b-button size="lg" variant="info">Sp. ATK</b-button>
      <b-button size="lg" variant="success">HEAL</b-button>
      <b-button size="lg" variant="warning">RUN</b-button>
    </div>


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
  justify-content: space-evenly;
  height: 100%;
  margin: 0 auto;
}

.player-space {
  width: 50%;
}
</style>
