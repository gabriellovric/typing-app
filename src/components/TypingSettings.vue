<script>
export default {
  data() {
    return {

      availableKeysets: [
        [[' ', 'q', 'w', 'e', 'r', 't'], 'Oberereihe links'],
        [[' ', 'z', 'u', 'i', 'o', 'p', 'ü'], 'Oberereihe rechts'],
        [[' ', 'a', 's', 'd', 'f', 'g'], 'Grundreihe links'],
        [[' ', 'h', 'j', 'k', 'l', 'ö', 'ä'], 'Grundreihe rechts'],
        [[' ', 'y', 'x', 'c', 'v', 'b'], 'Unterereihe links'],
        [[' ', 'n', 'm'], 'Unterereihe rechts']
      ],
      selectedKeysets: null,
      textLength: 200,
    }
  },
  methods: {
    start() {
      let keys = this.selectedKeysets.flat();
      this.$emit('start', [keys, this.textLength])
    }
  }
}
</script>

<template>
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

  <input v-model="textLength" />
  <button
    v-if="selectedKeysets"
    @click="start"
  >Start</button>
</template>
