<script setup lang="ts">
defineProps<{
  incorrectGuesses: number;
}>();
</script>

<template>
  <div class="grid place-items-center">
    Incorrect Guesses: {{ incorrectGuesses }}
    <div class="relative w-48 h-48">
      <!-- Base -->
      <div class="absolute bottom-0 w-full h-2 bg-pink-500"></div>
      <!-- Pole -->
      <div class="absolute bottom-0 left-1/4 w-2 h-full bg-pink-500"></div>
      <!-- Top -->
      <div class="absolute top-0 left-1/4 w-24 h-2 bg-pink-500"></div>
      <!-- Rope -->
      <div class="absolute top-0 right-1/4 w-2 h-12 bg-pink-500"></div>

      <!-- Head -->
      <div
        v-if="incorrectGuesses >= 1"
        class="absolute top-12 right-1/4 transform -translate-x-1/2 w-8 h-8 rounded-full border-4 border-cyan-400 animate-fade-in"
      ></div>
      <!-- Body -->
      <div
        v-if="incorrectGuesses >= 2"
        class="absolute top-20 right-1/4 transform -translate-x-1/2 w-2 h-16 bg-cyan-400 animate-fade-in"
      ></div>
      <!-- Left Arm -->
      <div
        v-if="incorrectGuesses >= 3"
        class="absolute top-24 right-1/4 transform -translate-x-1/2 w-8 h-2 bg-cyan-400 rotate-45 origin-right animate-fade-in"
      ></div>
      <!-- Right Arm -->
      <div
        v-if="incorrectGuesses >= 4"
        class="absolute top-24 right-1/4 transform -translate-x-1/2 w-8 h-2 bg-cyan-400 -rotate-45 origin-left animate-fade-in"
      ></div>
      <!-- Left Leg -->
      <div
        v-if="incorrectGuesses >= 5"
        class="absolute top-36 right-1/4 transform -translate-x-1/2 w-8 h-2 bg-cyan-400 rotate-45 origin-right animate-fade-in"
      ></div>
      <!-- Right Leg -->
      <div
        v-if="incorrectGuesses >= 6"
        class="absolute top-36 right-1/4 transform -translate-x-1/2 w-8 h-2 bg-cyan-400 -rotate-45 origin-left animate-fade-in"
      ></div>
    </div>
  </div>
</template>

<style scoped>
.animate-fade-in {
  animation: fadeIn 0.5s ease-in;
}

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: scale(0.8) translateX(-50%);
  }
  to {
    opacity: 1;
    transform: scale(1) translateX(-50%);
  }
}
</style>
