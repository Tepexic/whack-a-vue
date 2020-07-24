<template>
  <div id="app" class="h-screen w-full bg-orange-400 px-4 pt-4 text-yellow-100 shadow-lg md:px-40 md:pt-20">
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

    <h1 class="text-center text-3xl my-3 tracking-wider font-bolder">Whack-a-mole!</h1>
    
    <div class="md:w:3/5 flex justify-center items-center my-2">
      <div class="flex justify-between">
        <div class="mx-2"> 
          <div class="w-full text-center">Level</div>
          <div class="score px-2">10</div>
        </div>
        <div class="px-4 py-2 mx-4"> 
          <div class="w-full text-center">Time</div>
          <div class="score px-2">0:30</div>
        </div>
        <button class="rounded-lg px-4 py-2 mx-2 border-2 border-green-400 shadow-lg bg-green-500 hover:bg-green-600" >Start!</button>
      </div>
    </div>


    <div class="grid grid-rows-3">
      <div class="hole hole1">
        <div class="mole"></div>
      </div>
      <div class="hole hole2">
        <div class="mole"></div>
      </div>
      <div class="hole hole3">
        <div class="mole"></div>
      </div>
      <div class="hole hole4">
        <div class="mole"></div>
      </div>
      <div class="hole hole5">
        <div class="mole"></div>
      </div>
      <div class="hole hole6">
        <div class="mole"></div>
      </div>
    </div>

    <div class="game bg-yellow-300">
      <div class="hole hole1">
        <div class="mole"></div>
      </div>
      <div class="hole hole2">
        <div class="mole"></div>
      </div>
      <div class="hole hole3">
        <div class="mole"></div>
      </div>
      <div class="hole hole4">
        <div class="mole"></div>
      </div>
      <div class="hole hole5">
        <div class="mole"></div>
      </div>
      <div class="hole hole6">
        <div class="mole"></div>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  components: {
  }
}
</script>

<style>
@import 'assets/style.css';
</style>
