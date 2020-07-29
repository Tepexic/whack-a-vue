<template>
  <div class="hole h-24 flex justify-center">
    <transition name="moleMove">
      <img v-if="show" @click.prevent="whack" class="w-8/12 md:w-full lg:w-4/5" src="./../assets/mole.svg"/>
    </transition>
  </div>
</template>

<script>

export default {
  props: {
    id: {
      type:Number
    },
    show: {
      type: Boolean,
      default: false
    }
  },
  methods: {
    whack: function() {
      this.$emit('whacked', this.id)
    }
  }
}
</script>

<style>
.moleMove-enter-active {
  animation: popOut 0.25s ease-in;
}
@keyframes popOut {
  0%{
    transform: translateY(400px);
  }
  100%{
    transform: translateY(0px);
  }
}
.moleMove-leave-active {
  animation: popIn 0.25s ease-in;
}
@keyframes popIn {
  0%{
    transform: translateY(0px);
  }
  100%{
    transform: translateY(400px);
  }
}
</style>
