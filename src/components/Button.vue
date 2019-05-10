<template>
  <button v-on:click.stop.prevent="hit('default')">
    <slot>Attack</slot>
  </button>
</template>

<script>
export default {
    methods: {
        hit: function(message) {
            console.log(message)
        }
    }
};
</script>

<style>
button {
  width: 25%;
  height: 50px;
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  margin-top: 10px;
  margin-bottom: 10px;
}
</style>
