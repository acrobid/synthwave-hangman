<script setup lang="ts">
const KEYS = [
  ['Q', 'W', 'E', 'R', 'T', 'Y', 'U', 'I', 'O', 'P'],
  ['A', 'S', 'D', 'F', 'G', 'H', 'J', 'K', 'L'],
  ['Z', 'X', 'C', 'V', 'B', 'N', 'M']
]

const props = defineProps<{
  guessedLetters: string[]
  word: string
}>()

const emit = defineEmits<{
  (e: 'guess', letter: string): void
}>()

const getKeyStatus = (key: string) => {
  if (!props.guessedLetters.includes(key)) return 'unused'
  if (props.word.includes(key)) return 'correct'
  return 'wrong'
}
</script>

<template>
  <div class="grid gap-2">
    <div v-for="(row, index) in KEYS" :key="index" 
      class="flex justify-center gap-1">
      <button
        v-for="key in row"
        :key="key"
        @click="emit('guess', key)"
        :disabled="guessedLetters.includes(key)"
        :class="[
          'w-10 h-12 rounded font-bold transition-all duration-300',
          'hover:scale-110 hover:shadow-neon active:scale-95',
          {
            'bg-gray-700 text-gray-400': getKeyStatus(key) === 'unused',
            'bg-green-600 text-white': getKeyStatus(key) === 'correct',
            'bg-red-600 text-white': getKeyStatus(key) === 'wrong'
          }
        ]"
      >
        {{ key }}
      </button>
    </div>
  </div>
</template>