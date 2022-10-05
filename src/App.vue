<template>
  <h1>Ninja Reaction Timer</h1>
  <!-- <button @click="start" :disabled="isPlaying">Play</button> -->
  <div v-if="!isPlaying" class="play-button"  @click="start"></div>
  <Block v-if="isPlaying" :delay="delay" @end="endGame" />
  <Results v-if="showResults" :score="score" />
</template>

<script>
// when the game ends, show the results component
// output the score inside the results component

import Block from './components/Block'
import Results from './components/Results'

export default {
  name: 'App',
  components: { Block, Results },
  data() {
    return {
      isPlaying: false,
      delay: null,
      score: null,
      showResults: false,
      turns : 0
    }
  },
  methods: {
    start() {
      // set time amount (ms)
      this.delay = 20 + Math.random() * 50
      this.isPlaying = true
      this.showResults = false
      this.score = 0
      this.turns = 0
    },
    nextTurn() {
      // set time amount (ms)
      this.delay = 20 + Math.random() * 50
      this.isPlaying = true
      this.showResults = false
      
    },
    endGame(reactionTime) {
      this.score = this.score  + reactionTime
      this.turns ++
      console.log(this.turns + " - " + this.score )
      if(this.turns >10){
        
        this.showResults = true
        this.isPlaying = false
        
      }else{
        this.isPlaying = false
        this.nextTurn()
      }
      
      
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
  .play-button {
    color: white;
    border: none;
    width:50px;
    height:50px;
    /*padding: 8px 16px;
     border-radius: 4px; */
    font-size: 16px;
    letter-spacing: 1px;
    cursor: pointer;
    margin: 10px;
    background-image: url('assets/play.jpg');
  }
  button[disabled] {
    opacity: 0.2;
    cursor: not-allowed;
    
  }
</style>
