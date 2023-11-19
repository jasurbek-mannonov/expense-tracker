<script setup>
import { defineProps } from 'vue';

const props = defineProps({
    total: {
    type: Number,
    required: true
    },
})
</script>

<template>
    <h4>Hisobingiz</h4>
    <h1 id="balance">UZS {{ total }}</h1>
</template>