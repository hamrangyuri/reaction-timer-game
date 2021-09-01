<template>
  <h1>Reaction Timer</h1>
  <p>Hit play then click the green box when it shows up!</p>
  <button @click="startGame" :disabled="isPlaying">Play</button>
  <Block v-if="isPlaying" :delay="delay" @end-of-game="showResult" />
  <Result v-if="endGameScreen" :score="result" />
</template>

<script>
import Block from "./components/Block.vue";
import Result from "./components/Result.vue";

export default {
  name: "App",
  components: { Block, Result },
  data() {
    return {
      isPlaying: false,
      delay: null,
      result: null,
      endGameScreen: false,
    };
  },
  methods: {
    startGame() {
      this.endGameScreen = false;
      this.delay = 2000 + Math.random() * 2000;
      this.isPlaying = true;
      // console.log(`Game started with delay: ${this.delay}ms`);
    },
    showResult(reactionTime) {
      this.result = reactionTime;
      this.isPlaying = false;
      this.endGameScreen = true;
    },
  },
};
</script>

<style>
body {
  margin: 0;
  padding: 5px;
  overflow: hidden;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #444;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100vh;
}
button {
  background: #0faf87;
  color: white;
  border: none;
  padding: 8px 16px;
  border-radius: 4px;
  font-size: 16px;
  letter-spacing: 1px;
  cursor: pointer;
  margin: 10px;
}
button[disabled] {
  opacity: 0.2;
  cursor: not-allowed;
}
h1 {
  margin: 0;
  padding: 0;
}
p {
  margin-top: 0.5rem;
  padding: 0;
}
</style>
