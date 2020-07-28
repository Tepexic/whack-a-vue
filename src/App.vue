<template>
  <div id="app" class="h-screen w-full bg-purple-900 px-4 pt-4 text-yellow-100 shadow-lg md:px-48 md:pt-20">
    <div class="flex items-center justify-between">
      <div class="text-sm flex flex-col justify-center">
        <div class="tracking-wider text-center">HIGH SCORE</div>
        <div class="score">00000</div>
      </div>
      <div class="text-sm flex flex-col justify-center tracking-wider">
        <div class="tracking-wider text-center">YOUR SCORE</div>
        <div class="score">00000</div>
      </div>
    </div>

    <h1 class="text-center text-3xl my-3 tracking-wider font-bolder">Whack-a-<span class="text-green-500">Vue</span>!</h1>
    
    <div class="md:w:4/5 flex justify-center items-center my-4">
      <div class="flex justify-between items-center">
        <div class="mx-2"> 
          <div class="w-full text-center">Level</div>
          <div class="score px-2">10</div>
        </div>
        <div class="px-4 py-2 mx-4"> 
          <div class="w-full text-center">Time</div>
          <div class="score px-2">0:30</div>
        </div>
        <button @click="whack" class="rounded-lg px-4 py-2 mx-2 border-2 border-green-300 shadow-lg bg-green-500 hover:bg-green-300 hover:text-green-700" >Start!</button>
      </div>
    </div>


    <div class="grid grid-cols-3 md:gap-4 rounded shadow-lg md:4/5 bg-yellow-400 py-2">
      <Mole :show="mole"/>
    </div>
  </div>
</template>

<script>
import Mole from '@/components/Mole'

export default {
  name: 'App',

  data: function () {
    return {
      mole: true,
    }
  },
  components: {
    Mole
  },
  methods: {
    whack: function() {
      return this.mole = !this.mole
    }
  }

}
</script>

<style>
@import 'assets/style.css';
</style>
