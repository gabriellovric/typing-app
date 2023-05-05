<script>
export default {
  data() {
    return {
      availableKeysets: [
        [['q', 'w', 'e', 'r', 't', 'z', 'u', 'i', 'o', 'p', 'ü', ' '], 'Oberereihe'],
        [['a', 's', 'd', 'f', 'g', 'h', 'j', 'k', 'l', 'ö', 'ä', ' '], 'Grundreihe'],
        [['y', 'x', 'c', 'v', 'b', 'n', 'm', ' '], 'Unterereihe']
      ],
      keyset: null,
      textLength: 100,
      pointer: 0,
      text: null
    }
  },
  methods: {
    start() {
      this.pointer = 0;
      this.text = Array.from(
        { length: this.textLength },
        () => this.keyset[Math.floor(Math.random() * this.keyset.length)]);

      window.addEventListener('keyup', this.type)
    },
    type(event) {
      console.log(event)
      if (event.key === this.text[this.pointer]) {
        this.pointer++;
      }
    }
  }
}
</script>

<template>
  <main>
    <div v-if="!text">
      <select v-model="keyset">
        <option
          v-for="([key, value]) in availableKeysets"
          :value="key"
        >
          {{ value }}
        </option>
      </select>

      <select v-model="textLength">
        <option>100</option>
        <option>500</option>
        <option>1000</option>
      </select>

      <button
        v-if="keyset"
        @click="start"
      >Start</button>
    </div>

    <div
      v-if="text"
      class="text"
    >
      <span
        v-for="(key, i) in text"
        :class="{ active: pointer === i }"
      >{{ key }}</span>
    </div>

  </main>
</template>