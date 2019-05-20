<template>
  <div id="app">
    <div class="container">
      <div class="row">
        <div class="col-lg-5">
          <h3 v-if="!gameRunning">Player</h3>
          <h3 v-else>{{playerName}}</h3>
          <img class="player-sprite" src="./assets/adventurer/adventurer-idle-00.png">
          <p class="health-bar">{{playerHealth}}</p>
        </div>
        <div class="col-lg-1">
          <h5>VS</h5>
        </div>
        <div class="col-lg-5">
          <h3>Monster</h3>
          <img class="player-sprite" src="./assets/logo.png">
          <p class="health-bar">{{monsterHealth}}</p>
        </div>
      </div>
      <div class="row">
        <div id="controls" class="col-lg-12" v-if="gameRunning">
          <div v-bind:class="{ 'd-none': turn }">
            <span>Hello, {{playerName}}.</span>
            <span>Are you ready to begin?</span>
            <b-button variant="danger" @click="turn++">LET'S GO</b-button>
          </div>

          <div v-bind:class="{ 'd-none': !turn }">
            <b-button size="lg" variant="primary" v-on:click.stop.prevent="attack">ATK</b-button>
            <b-button size="lg" variant="info" @click="specialAttack">Sp. ATK</b-button>
            <b-button size="lg" variant="success" @click="heal">HEAL</b-button>
            <b-button size="lg" variant="warning" @click="runAway">RUN</b-button>
          </div>
        </div>

        <div id="start-prompt" class="col-lg-12" v-else>
          <template>
            <p>What is your name, brave adventurer?</p>
            <form class="form-inline justify-content-center" @submit.prevent="onSubmit">
              <b-form-input v-model="playerName" placeholder="Enter your name"></b-form-input>
              <button type="submit" class="btn btn-secondary">ENTER</button>
            </form>
          </template>
        </div>
      </div>
      <div class="row">
        <div id="action-log" class="col-lg-12 bg-dark text-light">
          <p>All the damage logs go here</p>
        </div>
      </div>
      <div class="row">
        <div id="credits" class="col-lg-12">
          Adventurer sprite assets courtesty of
          <strong>
            <a href="https://rvros.itch.io/animated-pixel-hero">rvros</a>
          </strong>
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
      playerName: "",
      turn: 0
    };
  },
  methods: {
    attack: function() {
      this.playerHealth -= this.calcDamage(7, 20);
      this.monsterHealth -= this.calcDamage(3, 10);
      this.checkWin();
    },
    specialAttack: function() {
      this.playerHealth -= this.calcDamage(7, 20);
      this.monsterHealth -= this.calcDamage(15, 35);
      this.checkWin();
    },
    heal: function() {
      this.playerHealth -= this.calcDamage(7, 15);
      this.playerHealth += this.calcDamage(10, 30);
      this.checkWin();
    },
    runAway: function() {
      alert("You ran away like a coward. The monster ate you anyway.");
      this.playerHealth = 0;
      this.checkWin();
    },
    calcDamage: function(min, max) {
      return Math.max(Math.floor(Math.random() * max), min);
    },
    onSubmit: function() {
      this.gameRunning = true;
      this.playerHealth = 100;
      this.monsterHealth = 100;
    },
    checkWin: function() {
      if (this.monsterHealth <= 0 && this.playerHealth <= 0) {
        alert("Double death!");
        this.monsterHealth = 0;
        this.playerHealth = 0;
        this.gameRunning = false;
        return false;
      } else if (this.monsterHealth <= 0) {
        this.gameRunning = false;
        this.monsterHealth = 0;
        alert("You are victorious!");
        return true;
      } else if (this.playerHealth <= 0) {
        alert("GAME OVER! You died");
        this.gameRunning = false;
        this.playerHealth = 0;
        return false;
      } else return false;
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

#action-log {
  height: 30em;
}

div {
  padding: 5px;
}

.health-bar {
  vertical-align: text-bottom;
}

img.player-sprite {
  min-width: 20%;
  min-height: 20%;
}
</style>
