<script setup lang="ts">
defineProps<{
  incorrectGuesses: number;
}>();
</script>

<template>
  <div class="grid place-items-center">
    <div class="text-sm text-pink-200 mb-2">Incorrect Guesses: {{ incorrectGuesses }}</div>

    <svg
      class="hangman-svg"
      viewBox="0 0 120 160"
      xmlns="http://www.w3.org/2000/svg"
      role="img"
      aria-label="Hangman drawing"
    >
      <!-- Gallows -->
      <line x1="10" y1="150" x2="110" y2="150" class="gallows" />
      <line x1="30" y1="150" x2="30" y2="10" class="gallows" />
      <line x1="30" y1="10" x2="80" y2="10" class="gallows" />
      <line x1="80" y1="10" x2="80" y2="30" class="gallows" />

      <!-- Head -->
      <circle
        v-if="incorrectGuesses >= 1"
        cx="80"
        cy="44"
        r="12"
        class="hangman-part visible"
      />

      <!-- Body -->
      <line
        v-if="incorrectGuesses >= 2"
        x1="80"
        y1="56"
        x2="80"
        y2="100"
        class="hangman-part visible"
      />

      <!-- Left arm -->
      <line
        v-if="incorrectGuesses >= 3"
        x1="80"
        y1="68"
        x2="62"
        y2="86"
        class="hangman-part visible"
      />

      <!-- Right arm -->
      <line
        v-if="incorrectGuesses >= 4"
        x1="80"
        y1="68"
        x2="98"
        y2="86"
        class="hangman-part visible"
      />

      <!-- Left leg -->
      <line
        v-if="incorrectGuesses >= 5"
        x1="80"
        y1="100"
        x2="66"
        y2="130"
        class="hangman-part visible"
      />

      <!-- Right leg -->
      <line
        v-if="incorrectGuesses >= 6"
        x1="80"
        y1="100"
        x2="94"
        y2="130"
        class="hangman-part visible"
      />
    </svg>
  </div>
</template>

<style scoped>
.hangman-svg {
  width: 10rem;
  height: 12rem;
  overflow: visible;
}

.gallows {
  stroke: #ff4da6; /* pink */
  stroke-width: 4;
  stroke-linecap: round;
}

.hangman-part {
  stroke: #00fff0; /* cyan */
  stroke-width: 4;
  stroke-linecap: round;
  stroke-linejoin: round;
  fill: none;
  opacity: 0;
  transform-origin: center;
  transition: opacity 220ms ease, transform 220ms ease;
}

.hangman-part.visible {
  opacity: 1;
  transform: none;
}</style>