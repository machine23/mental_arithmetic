<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <start-screen v-if="state == 'start'" @onStart="onStart"/>
    <training v-else-if="state == 'training'" @onStop="onStop"/>
    <div v-else>Error</div>
  </div>
</template>

<script>
import StartScreen from "./components/StartScreen.vue";
import Training from "./components/Training.vue";

export default {
  name: "app",
  components: {
    StartScreen,
    Training
  },
  data() {
    return {
      state: "start"
    };
  },
  methods: {
    onStart() {
      this.state = "training";
    },
    onStop() {
      this.state = "start";
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  text-align: center;
  margin-top: 60px;
}
</style>
