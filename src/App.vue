<script setup>
import { ref } from 'vue';
import TypingPrompt from './components/TypingPrompt.vue';
import TypingSettings from './components/TypingSettings.vue';

const text = ref([])

function startTyping([keys, length]) {
  let randomKey = () => keys[Math.floor(Math.random() * keys.length)];
  text.value = Array.from({ length: length }, randomKey);
}

function done(_stats) {
  text.value = "";
}

</script>

<template>
  <TypingSettings
    v-if="text.length === 0"
    @start="startTyping"
  />
  <TypingPrompt
    v-if="text.length > 0"
    :text="text"
    @done="done"
  />
</template>