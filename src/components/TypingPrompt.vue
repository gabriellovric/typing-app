<script>
export default {
    data() {
        return {
            pointer: 0,
        };
    },
    props: {
        text: String
    },
    methods: {
        validateKey(event) {
            if (event.key === this.text[this.pointer]) {
                this.pointer++;
            }
        }
    },
    mounted() {
        window.addEventListener('keyup', this.validateKey)
    },
    unmounted() {
        window.removeEventListener('keyup', this.validateKey);
    }
}
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