<script setup>
import { defineProps } from 'vue';

const props = defineProps({
    income: {
        type: Number,
        required: true
    },
    expense: {
        type: Number,
        required: true
    }
})
</script>

<template>
    <div class="inc-exp-container">
        <div>
            <h4>Kirim</h4>
            <p id="money-plus" class="money plus">+UZS {{income}}</p>
        </div>
        <div>
            <h4>Chiqim</h4>
            <p id="money-minus" class="money minus">UZS{{expense}}</p>
        </div>
    </div>
</template>