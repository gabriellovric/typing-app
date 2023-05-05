<script>
import TypingPrompt from './components/TypingPrompt.vue';
import TypingSettings from './components/TypingSettings.vue';

export default {
  data() {
    return {
      text: null,
    };
  },
  methods: {
    startTyping([keys, length]) {
      let a = () => {
        return keys[Math.floor(Math.random() * keys.length)]
      }
      this.text = Array.from({ length: length }, a);
      console.log(this.text)
    },
  },
  components: { TypingSettings, TypingPrompt }
}
</script>

<template>
  <TypingSettings
    v-if="!text"
    @start="startTyping"
  />
  <TypingPrompt
    v-if="text"
    :text="text"
  />
</template>