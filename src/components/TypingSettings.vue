<script setup>
import { ref } from 'vue';

const emit = defineEmits({ start: null })

const availableKeysets = [
  [[' ', 'q', 'w', 'e', 'r', 't'], 'Oberereihe links'],
  [[' ', 'z', 'u', 'i', 'o', 'p', 'ü'], 'Oberereihe rechts'],
  [[' ', 'a', 's', 'd', 'f', 'g'], 'Grundreihe links'],
  [[' ', 'h', 'j', 'k', 'l', 'ö', 'ä'], 'Grundreihe rechts'],
  [[' ', 'y', 'x', 'c', 'v', 'b'], 'Unterereihe links'],
  [[' ', 'n', 'm'], 'Unterereihe rechts']
];
const selectedKeysets = ref([])
const textLength = ref(200)

function start() {
  let keys = selectedKeysets.value.flat();
  emit('start', [keys, textLength.value])
}
</script>

<template>
  <form>
    <select
      v-model="selectedKeysets"
      multiple
    >
      <option
        v-for="([key, value]) in availableKeysets"
        :value="key"
      >
        {{ value }}
      </option>
    </select>

    <label for="textLength">
      Text Length
      <input
        type="number"
        id="textLength"
        v-model="textLength"
        required
      />
    </label>
    <button
      v-if="selectedKeysets.length > 0"
      @click="start"
    >Start</button>
  </form>
</template>
