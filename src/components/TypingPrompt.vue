<script setup>
import { onMounted, onUnmounted, ref } from 'vue';

const props = defineProps({ text: Array });
const emit = defineEmits({ done: Array })

const pointer = ref(0);
const errorCount = ref(0);
const elapsedSeconds = ref(0);

let interval = null;

function validateKey(event) {
    if (event.key === props.text[pointer.value]) {
        pointer.value++;
        if (props.text.length == pointer.value) {
            emit('done', [errorCount.value, elapsedSeconds.value])
        }
    }
    else {
        errorCount.value++
    }
}

onMounted(() => {
    window.addEventListener('keyup', validateKey);
    interval = setInterval(() => { elapsedSeconds.value++ }, 1000)
});
onUnmounted(() => {
    window.removeEventListener('keyup', validateKey)
    clearInterval(interval)
});
</script>

<template>
    <div>
        <span
            v-for="(key, i) in text"
            :class="{ active: pointer === i }"
        >{{ key }}</span>
    </div>
    <p>
        Errors: {{ errorCount }}
    </p>
    <p>
        {{ Math.floor(elapsedSeconds / (3600 * 24)) }} :
        {{ Math.floor((elapsedSeconds % (3600 * 24)) / 3600) }} :
        {{ Math.floor((elapsedSeconds % 3600) / 60) }} :
        {{ elapsedSeconds % 60 }}
    </p>
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