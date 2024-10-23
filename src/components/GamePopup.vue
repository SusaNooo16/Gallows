<script setup lang="ts">
interface Props {
  isWin: boolean
  word: string
}
defineProps<Props>()

interface Emit {
  (event: string): void
}

defineEmits<Emit>()
</script>
<template>
  <div class="popup-container">
    <div class="popup">
      <h2 v-if="isWin">Поздравляю, вы победили! 😃</h2>
      <h2 v-else>Вы проиграли. 😕</h2>
      <h3>...имя: {{ word.charAt(0).toUpperCase() + word.slice(1) }}</h3>
      <button @click="$emit('playAgain')">Сыграть еще раз</button>
    </div>
  </div>
</template>
