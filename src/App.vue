<script setup lang="ts">
import { ref, computed } from 'vue';
import {
  DialogRoot,
  DialogContent,
  DialogTitle,
  DialogTrigger,
} from 'radix-vue';
import HangmanDrawing from './components/HangmanDrawing.vue';
import Keyboard from './components/Keyboard.vue';
import { useStorage } from '@vueuse/core';

const words = [
  'TYPESCRIPT',
  'JAVASCRIPT',
  'PROGRAMMING',
  'COMPUTER',
  'DEVELOPER',
  'HANGMAN',
  'SYNTHWAVE',
  'CYBERPUNK',
];

const word = ref(words[Math.floor(Math.random() * words.length)]);
const guessedLetters = ref<string[]>([]);
const incorrectGuesses = ref(0);
const gameStatus = ref<'playing' | 'won' | 'lost'>('playing');
const highScore = useStorage('hangman-highscore', 0);

const maskedWord = computed(() => {
  return word.value
    .split('')
    .map((letter) => (guessedLetters.value.includes(letter) ? letter : '_'))
    .join(' ');
});

const isWinner = computed(() => {
  return word.value
    .split('')
    .every((letter) => guessedLetters.value.includes(letter));
});

const handleGuess = (letter: string) => {
  if (gameStatus.value !== 'playing') return;

  if (!guessedLetters.value.includes(letter)) {
    guessedLetters.value.push(letter);
    if (!word.value.includes(letter)) {
      incorrectGuesses.value++;
      if (incorrectGuesses.value >= 6) {
        gameStatus.value = 'lost';
      }
    }
  }

  if (isWinner.value) {
    gameStatus.value = 'won';
    const score = Math.max(0, 100 - incorrectGuesses.value * 10);
    if (score > highScore.value) {
      highScore.value = score;
    }
  }
};

const resetGame = () => {
  word.value = words[Math.floor(Math.random() * words.length)];
  guessedLetters.value = [];
  incorrectGuesses.value = 0;
  gameStatus.value = 'playing';
};
</script>

<template>
  <div
    class="min-h-screen bg-gradient-to-br from-purple-900 via-indigo-800 to-pink-800 text-white p-8"
  >
    <div class="max-w-4xl mx-auto grid grid-cols-1 gap-8">
      <header class="text-center">
        <h1 class="text-6xl font-bold mb-4 animate-glow">Synthwave Hangman</h1>
        <p class="text-xl text-pink-300">High Score: {{ highScore }}</p>
      </header>

      <HangmanDrawing :incorrect-guesses="incorrectGuesses" />

      <div class="text-center">
        <p class="text-4xl font-mono tracking-wider mb-4 neon-text">
          {{ maskedWord }}
        </p>
      </div>

      <Keyboard
        :guessed-letters="guessedLetters"
        :word="word"
        @guess="handleGuess"
      />

      <DialogRoot :open="gameStatus !== 'playing'" modal>
        <DialogContent class="bg-purple-900 p-6 rounded-lg shadow-neon">
          <DialogTitle class="text-3xl font-bold mb-4">
            {{ gameStatus === 'won' ? '🎉 Congratulations!' : '💀 Game Over' }}
          </DialogTitle>
          <p class="mb-4">
            {{
              gameStatus === 'won'
                ? `You won! Score: ${Math.max(0, 100 - incorrectGuesses * 10)}`
                : `The word was: ${word}`
            }}
          </p>
          <button
            @click="resetGame"
            class="px-4 py-2 bg-pink-600 hover:bg-pink-700 rounded transition-colors"
          >
            Play Again
          </button>
        </DialogContent>
      </DialogRoot>
    </div>
  </div>
</template>

<style>
.animate-glow {
  animation: glow 2s ease-in-out infinite alternate;
}

@keyframes glow {
  from {
    text-shadow: 0 0 10px #fff, 0 0 20px #fff, 0 0 30px #e60073,
      0 0 40px #e60073, 0 0 50px #e60073, 0 0 60px #e60073, 0 0 70px #e60073;
  }
  to {
    text-shadow: 0 0 20px #fff, 0 0 30px #ff4da6, 0 0 40px #ff4da6,
      0 0 50px #ff4da6, 0 0 60px #ff4da6, 0 0 70px #ff4da6, 0 0 80px #ff4da6;
  }
}

.shadow-neon {
  box-shadow: 0 0 10px #e60073, 0 0 20px #e60073, 0 0 30px #e60073;
}

.neon-text {
  text-shadow: 0 0 10px #fff, 0 0 20px #fff, 0 0 30px #0ff;
}
</style>
