<template>
  <h1 v-if="!isPlaying">How fast you are?</h1>
  <h1 v-else>...</h1>
  <button @click="start" :disabled="isPlaying">Play</button>
  <Block v-if="isPlaying" :delay="delay" @end="endGame"/>
  <Results v-else-if="showResults" :score="score"/>
</template>

<script>
import { toHandlerKey } from '@vue/shared'
import Block from './components/Block.vue'
import Results from './components/Results.vue'

export default {
  name: 'App',
  components: { Block, Results},
  data() {
    return {
      isPlaying: false,
      delay: null,
      score: 0,
      showResults: false
    }
  },
  methods: {
    start() {
      this.delay = 2000 + Math.random() * 5000
      this.isPlaying = true
      this.showResults = false
    },
    endGame(reactionTime) {
      this.score = reactionTime
      this.isPlaying = false
      this.showResults = true
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #444;
  margin-top: 60px;
}

button {
  background: rgb(44, 42, 42);
  color: white;
  border: none;
  padding: 8px 16px;
  border-radius: 5px;
  font-size: 15px;
  letter-spacing: 1px;
  cursor: pointer;
  margin: 10px;
  }
button[disabled] {
  opacity: 0,2;
  cursor: not-allowed;
}
</style>
