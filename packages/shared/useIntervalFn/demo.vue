<script setup lang="ts">
import { ref } from 'vue'
import { useIntervalFn } from '@vueuse/core'

const greetings = ['Hello', 'Hi', 'Yo!', 'Hey', 'Hola', 'こんにちは', 'Bonjour', 'Salut!', '你好']
const word = ref('Hello')
const interval = ref(500)

const { pause, resume, isActive } = useIntervalFn(() => {
  word.value = greetings[Math.round(Math.random() * (greetings.length - 1))]
}, interval)
</script>

<template>
  <p>{{ word }}</p>
  <p>
    interval:
    <input v-model="interval" type="number" placeholder="interval">
  </p>
  <button v-if="isActive" class="orange" @click="pause">
    Pause
  </button>
  <button v-if="!isActive" @click="resume">
    Resume
  </button>
</template>
