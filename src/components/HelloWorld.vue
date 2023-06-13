<script setup>
import { ref } from 'vue'

defineProps({
    msg: String,
})

const styles = import.meta.glob('../dynamic*.scss', { query: '?inline' });
const styleElem = document.createElement('style');
document.head.appendChild(styleElem);

async function loadStyle(name) {
    const { default: style } = await styles[`../${name}.scss`]();
    styleElem.textContent = style;
}

</script>

<template>
    <h1>{{ msg }}</h1>

    <div class="card">
        <button type="button" @click="loadStyle('dynamic')">Load SCSS 1 dynamically</button>
        <button type="button" @click="loadStyle('dynamic2')">Load SCSS 2 dynamically</button>
        <p>
            Edit
            <code>components/HelloWorld.vue</code> to test HMR
        </p>
    </div>

    <p>
        Check out
        <a href="https://vuejs.org/guide/quick-start.html#local" target="_blank">create-vue</a>, the official Vue + Vite
        starter
    </p>
    <p>
        Install
        <a href="https://github.com/vuejs/language-tools" target="_blank">Volar</a>
        in your IDE for a better DX
    </p>
    <p class="read-the-docs">Click on the Vite and Vue logos to learn more</p>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
