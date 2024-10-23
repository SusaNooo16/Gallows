<script setup lang="ts">
import GameHeader from './components/GameHeader.vue'
import GamePopup from './components/GamePopup.vue'
import GameNotification from './components/GameNotification.vue'
import { computed, ref } from 'vue'
import GameFigure from './components/GameFigure.vue'
import GameWrongLetters from './components/GameWrongLetters.vue'
import GameWord from './components/GameWord.vue'

const countWrongForLose = 5
const word = ref('кристина')
const letters = ref<string[]>([])
const normalizeWord = computed(() => Array.from(new Set(word.value.split(''))))
const correctLetters = computed(() =>
  letters.value.filter(x => word.value.includes(x)),
)
const wrongLetters = computed(() =>
  letters.value.filter(x => !word.value.includes(x)),
)
const isWin = computed(
  () => normalizeWord.value.length == correctLetters.value.length,
)
const isLose = computed(() => countWrongForLose == wrongLetters.value.length)
const isGameOver = computed(() => isWin.value || isLose.value)

const isNotificationShow = ref<boolean>(false)

window.addEventListener('keydown', ({ key }) => {
  if (/[А-Яа-я]/.test(key) && !isGameOver.value) {
    if (!letters.value.includes(key)) {
      letters.value.push(key.toLocaleLowerCase())
    } else {
      showNotification()
    }
  }
})

function showNotification(): void {
  isNotificationShow.value = true
}

function playAgain() {
  word.value = 'кристина'
  letters.value = []
}
</script>

<template>
  <div id="app">
    <GameHeader />

    <div class="game-container">
      <GameFigure :count-of-wrong-letters="wrongLetters.length" />
      <GameWrongLetters :wrong-letters="wrongLetters" />
      <GameWord :word="word" :correct-letters="correctLetters" />
    </div>

    <GamePopup
      v-if="isGameOver"
      :is-win="isWin"
      :word="word"
      @playAgain="playAgain"
    />
    <GameNotification v-model="isNotificationShow" />
  </div>
</template>
