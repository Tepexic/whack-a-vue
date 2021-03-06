<template>
  <div id="app" class="h-screen w-full bg-purple-900 px-4 pt-4 text-yellow-100 shadow-lg md:px-48 md:pt-20 lg:px-60">
    <div class="border-2 border-gray-200 bg-gray-900 p-2 md:p-8 rounded-lg shadow-lg">
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

      <h1 class="text-center text-3xl my-4 tracking-wider font-bolder">Whack-a-<span class="text-green-500">Vue</span>!</h1>
      
      <div class="md:w:4/5 flex justify-center items-center my-4 bg-orange-600 rounded shadow-inner">
        <div class="flex justify-between items-center">
          <div class="mx-2"> 
            <div class="w-full text-center">Level</div>
            <div class="score px-2">{{level}}</div>
          </div>
          <div class="px-4 py-2 mx-4"> 
            <div class="w-full text-center">Time</div>
            <div class="score px-2">{{displaySecondsLeft}}</div>
          </div>
          <button @click="startGame" class="rounded-lg px-4 py-2 mx-2 shadow-lg bg-green-500 hover:bg-green-300 hover:text-green-700" >Start!</button>
        </div>
      </div>


      <div class="grid grid-cols-3 md:gap-4 rounded shadow-inner md:4/5 bg-yellow-400 p-2">
        <Mole v-for="m in moles" v-on:whacked="bonk" :id="m.id" :show="m.show" :key="m.id"/>
      </div>
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
      timeUp: false,
      countdown: 0,
      seconds: 10,
      secondsLeft: 0,
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
    displaySecondsLeft: function () {
      return this.displayTimeLeft(this.secondsLeft)
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
    startGame: function () {
      this.score = 0;
      this.level = 1;
      this.runLevel()
    },

    runLevel: function () {
      this.timeUp = false;
      this.secondsLeft = this.seconds
      this.timer()
      setTimeout( () => {
        this.timeUp = true
        }, this.seconds * 1000)
      this.peep()
    },

    peep: function () {
      this.time = this.getTime(83.33 * (1 - this.level) + 1000, 111.11*(1 - this.level) + 1500)
      const hole = this.getHole()
      hole.show = true
      setTimeout( () => {
        hole.show = false;
        if(! this.timeUp) {
          this.peep()
        } else {
          if(this.level === 10) return
          this.level ++
          this.runLevel()
        }
        },
        this.time);
    },

    bonk: function(id) {
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

    getHole: function () {
      // Get a random hole, don't repeat last one
      let hole
      do {
        const idx = Math.floor( Math.random() * this.moles.length )
        hole = this.moles[idx];
      } while (hole === this.lastHole)
      this.lastHole = hole;
      return hole
    },

    fillWithZeros: function (max, score) {
      const ss = score.toString().split('');
      for (let k=0; k<=max-ss.length; k++) {
        ss.unshift('0')
      }
      return ss.join('')
    },

    timer: function () {
      // Clear, if any, the intervals
      if(this.countdown) clearInterval(this.countdown)
      const now = Date.now();
      const later =  now + this.seconds * 1000
      this.countdown = setInterval( () => {
        this.secondsLeft = Math.round((later - Date.now()) / 1000);
        if (this.secondsLeft < 0) {
          clearInterval(this.countdown)
          this.secondsLeft = 0;
          return
        }
      }, 1000)
    },

    displayTimeLeft: function (seconds) {
      const minutes = Math.floor( seconds / 60 )
      let remSeconds = seconds % 60
      if(remSeconds < 10) {
        remSeconds = '0' + remSeconds
      }
      return `${minutes}:${remSeconds}`
    }
  }

}
</script>

<style>
@import 'assets/style.css';
</style>
