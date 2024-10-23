<script setup lang="ts">
interface Props {
  word: string
  correctLetters: string[]
}
defineProps<Props>()
</script>
<template>
  <div class="word">
    <span v-for="(letter, index) in word" :key="index" class="letter">
      <template v-if="correctLetters.includes(letter)">
        {{ letter }}
      </template>
    </span>
  </div>
</template>
