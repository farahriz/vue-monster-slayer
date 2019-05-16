<template>
  <div id="app">
    <div class="container">
      <div class="row">
        <div class="col-lg-5">
          <h3>Player</h3>
          <p>{{playerHealth}}</p>
        </div>
        <div class="col-lg-1">
          <h5>VS</h5>
        </div>
        <div class="col-lg-5">
          <h3>Monster</h3>
          <p>{{monsterHealth}}</p>
        </div>
      </div>
      <div class="row">
        <div id="controls" class="col-lg-12" v-if="gameRunning">
          <b-button size="lg" variant="primary" v-on:click.stop.prevent="attack">ATK</b-button>
          <b-button size="lg" variant="info" @click="specialAttack">Sp. ATK</b-button>
          <b-button size="lg" variant="success" @click="heal">HEAL</b-button>
          <b-button size="lg" variant="warning">RUN</b-button>
        </div>

        <div id="start-prompt" class="col-lg-12" v-else>
          <template v-if="!playerName">
            <p>What is your name, brave adventurer?</p>
            <form class="form-inline justify-content-center">
              <b-form-input v-model="playerName" placeholder="Enter your name"></b-form-input>
              <b-button>ENTER</b-button>
            </form>
          </template>
          <template v-else>
            <span>Hello, {{playerName}}</span>
            <span>Are you ready to begin?</span>
            <b-button size="lg" variant="danger">LET'S GO</b-button>
          </template>
        </div>
      </div>
      <div class="row">
        <div id="action-log" class="col-lg-12 bg-dark text-light">
          <p>All the damage logs go here</p>
        </div>
      </div>
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
      playerHealth: 100,
      gameRunning: false,
      playerDeath: false,
      playerName: ""
    };
  },
  methods: {
    attack: function() {
      this.playerHealth -= this.calcDamage(7, 20);
      this.monsterHealth -= this.calcDamage(3, 10);
    },
    specialAttack: function() {
      this.playerHealth -= this.calcDamage(7, 20);
      this.monsterHealth -= this.calcDamage(15, 35);
    },
    heal: function() {
      this.playerHealth -= this.calcDamage(7, 15);
      this.playerHealth += this.calcDamage(10, 30);
    },
    calcDamage: function(min, max) {
      return Math.max(Math.floor(Math.random() * max), min);
    }
  }
};
</script>

<style scoped>
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
