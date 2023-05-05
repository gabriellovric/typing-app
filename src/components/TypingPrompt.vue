<script setup>
import { onMounted, onUnmounted, ref } from 'vue';

const props = defineProps({ text: Array });
const pointer = ref(0);

function validateKey(event) {
    if (event.key === props.text[pointer.value]) {
        pointer.value++;
    }
}

onMounted(() => window.addEventListener('keyup', validateKey));
onUnmounted(() => window.removeEventListener('keyup', validateKey));
</script>

<template>
    <span
        v-for="(key, i) in text"
        :class="{ active: pointer === i }"
    >{{ key }}</span>
</template>

<style scoped>
span {
    font-size: 2rem;
    white-space: pre-wrap;
}

.active {
    background-color: yellow;
}
</style>