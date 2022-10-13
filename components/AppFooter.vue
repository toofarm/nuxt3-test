<template>
    <footer>
        Made with love by Shane - {{ state.year }}
    </footer>
</template>

<script setup lang="ts">
import { reactive, onMounted } from 'vue'

const state = reactive({ year: 2021 })

onMounted(() => {
	const date = new Date()
	state.year = date.getFullYear()
})

</script>

<style>
    footer {
        border-top: 1px solid #ccc;
        background-color: #eee;
        padding: 1rem;
        font-size: 12px;
        color: #aaa;
    }
</style>