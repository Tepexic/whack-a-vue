<template>
  <div id="app" class="h-screen w-full bg-purple-900 px-4 pt-4 text-yellow-100 shadow-lg md:px-48 md:pt-20 lg:px-60">
    <div class="flex items-center justify-between">
      <div class="text-sm flex flex-col justify-center">
        <div class="tracking-wider text-center">HIGH SCORE</div>
        <div class="score">{{displayHighScore}}</div>
      </div>
      <div class="text-sm flex flex-col justify-center tracking-wider">
        <div class="tracking-wider text-center">YOUR SCORE</div>
        <div class="score">{{displayScore}}</div>
      </div>
    </div>

    <h1 class="text-center text-3xl my-3 tracking-wider font-bolder">Whack-a-<span class="text-green-500">Vue</span>!</h1>
    
    <div class="md:w:4/5 flex justify-center items-center my-4">
      <div class="flex justify-between items-center">
        <div class="mx-2"> 
          <div class="w-full text-center">Level</div>
          <div class="score px-2">{{level}}</div>
        </div>
        <div class="px-4 py-2 mx-4"> 
          <div class="w-full text-center">Time</div>
          <div class="score px-2">0:30</div>
        </div>
        <button @click="peep" class="rounded-lg px-4 py-2 mx-2 border-2 border-green-300 shadow-lg bg-green-500 hover:bg-green-300 hover:text-green-700" >Start!</button>
      </div>
    </div>


    <div class="grid grid-cols-3 md:gap-4 rounded shadow-lg md:4/5 bg-yellow-400 py-2">
      <Mole v-for="m in moles" v-on:whacked="bonk" :id="m.id" :show="m.show" :key="m.id"/>
    </div>
  </div>
</template>

<script>
import Mole from '@/components/Mole'

export default {
  name: 'App',

  data: function () {
    return {
      highScore: 0,
      score: 0,
      time: 0,
      timeUp: 30000,
      level: 1,
      lastHole: null,
      moles: [
        {id:0, show: false},
        {id:1, show: false},
        {id:2, show: false},
        {id:3, show: false},
        {id:4, show: false},
        {id:5, show: false},
      ]
    }
  },

  computed: {
    displayScore: function () {
      return this.fillWithZeros(8, this.score)
    },
    displayHighScore: function () {
      return this.fillWithZeros(8, this.highScore)
    },
  },

  mounted: function () {
    // Retrieve high score
    this.highScore = 0 | JSON.parse(localStorage.getItem('highScore'))
  },

  components: {
    Mole
  },

  methods: {
    bonk: function(id) {
      console.log(id)
      this.moles[id].show = false
      this.score += this.level * 10
      if(this.score > this.highScore) {
        this.highScore = this.score
        localStorage.setItem('highScore', this.highScore)
      }
    },
    
    getTime: function (min, max) {
      // get a random time
      return Math.round(Math.random() * (max - min) + min); // map random to [max, min]
    },

    peep: function () {
      // Get randorm time and hole
      this.time = this.getTime(300, 1000)/// (this.level * 0.5)
      const hole = this.getHole()
      hole.show = true
      setTimeout( () => {
        hole.show = false;
        if(! this.timeUp) this.peep();
        } , this.time);
    },

    getHole: function () {
      // Get a random hole, don't repeat last one
      let hole
      do {
        const idx = Math.floor( Math.random() * this.moles.length )
        hole = this.moles[idx];
      } while (hole === this.lastHole)
      this.lastHole = hole;
      console.log(hole.id)
      return hole
    },

    fillWithZeros: function (max, score) {
      const ss = score.toString().split('');
      for (let k=0; k<=max-ss.length; k++) {
        ss.unshift('0')
      }
      return ss.join('')
    }
  }

}
</script>

<style>
@import 'assets/style.css';
</style>
