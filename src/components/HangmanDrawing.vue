<script setup lang="ts">
defineProps<{
  incorrectGuesses: number;
}>();
</script>

<template>
  <div class="flex flex-col items-center gap-4">
    <p class="text-xl text-cyan-300">Incorrect Guesses: {{ incorrectGuesses }} / 6</p>
    <div class="relative w-64 h-64">
      <!-- Gallows Base -->
      <div class="absolute bottom-0 left-0 w-full h-2 bg-pink-500"></div>
      
      <!-- Gallows Pole -->
      <div class="absolute bottom-0 left-16 w-2 h-48 bg-pink-500"></div>
      
      <!-- Gallows Top Bar -->
      <div class="absolute top-0 left-16 w-32 h-2 bg-pink-500"></div>
      
      <!-- Gallows Rope -->
      <div class="absolute top-2 left-[11.5rem] w-2 h-12 bg-pink-500"></div>

      <!-- Head -->
      <div
        v-if="incorrectGuesses >= 1"
        class="absolute top-14 left-[10.5rem] w-10 h-10 rounded-full border-4 border-cyan-400 animate-fade-in"
      ></div>
      
      <!-- Body -->
      <div
        v-if="incorrectGuesses >= 2"
        class="absolute top-24 left-[11.75rem] w-2 h-16 bg-cyan-400 animate-fade-in"
      ></div>
      
      <!-- Left Arm -->
      <div
        v-if="incorrectGuesses >= 3"
        class="absolute top-28 left-[10rem] w-12 h-2 bg-cyan-400 origin-right rotate-45 animate-fade-in"
      ></div>
      
      <!-- Right Arm -->
      <div
        v-if="incorrectGuesses >= 4"
        class="absolute top-28 left-[12rem] w-12 h-2 bg-cyan-400 origin-left -rotate-45 animate-fade-in"
      ></div>
      
      <!-- Left Leg -->
      <div
        v-if="incorrectGuesses >= 5"
        class="absolute top-40 left-[10.25rem] w-10 h-2 bg-cyan-400 origin-right rotate-45 animate-fade-in"
      ></div>
      
      <!-- Right Leg -->
      <div
        v-if="incorrectGuesses >= 6"
        class="absolute top-40 left-[12rem] w-10 h-2 bg-cyan-400 origin-left -rotate-45 animate-fade-in"
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
    transform: scale(0.8);
  }
  to {
    opacity: 1;
    transform: scale(1);
  }
}
</style>
