<script setup lang="ts">
import { watch } from 'vue'

interface Props {
  modelValue: boolean
}

const props = defineProps<Props>()

const emit = defineEmits(['update:modelValue'])

let timerNotification: number = -1
function closeNotification(): void {
  clearTimeout(timerNotification)
  timerNotification = -1
  emit('update:modelValue', false)
}

watch(
  () => props.modelValue,
  newVal => {
    if (!newVal) {
      return
    }

    timerNotification = setTimeout(() => {
      closeNotification()
    }, 1000)
  },
)
</script>
<template>
  <div class="notification-container" :class="{ show: modelValue }">
    <p>Вы уже вводили этот символ</p>
  </div>
</template>
