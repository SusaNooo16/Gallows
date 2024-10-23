<script setup lang="ts">
interface Props {
  countOfWrongLetters: number
}

defineProps<Props>()
</script>
<template>
  <svg height="250" width="200" class="figure-container">
    <template v-if="countOfWrongLetters > 0">
      <!-- Rod -->
      <line x1="60" y1="20" x2="140" y2="20" />
      <line x1="140" y1="20" x2="140" y2="50" />
      <line x1="60" y1="20" x2="60" y2="230" />
      <line x1="20" y1="230" x2="100" y2="230" />
    </template>
    <template v-if="countOfWrongLetters > 1">
      <!-- Head -->
      <circle cx="140" cy="70" r="20" />
    </template>
    <template v-if="countOfWrongLetters > 2">
      <!-- Body -->
      <line x1="140" y1="90" x2="140" y2="150" />
    </template>
    <template v-if="countOfWrongLetters > 3">
      <!-- Arms -->
      <line x1="140" y1="120" x2="120" y2="100" />
      <line x1="140" y1="120" x2="160" y2="100" />
    </template>
    <template v-if="countOfWrongLetters > 4">
      <!-- Legs -->
      <line x1="140" y1="150" x2="120" y2="180" />
      <line x1="140" y1="150" x2="160" y2="180" />
    </template>
  </svg>
</template>
