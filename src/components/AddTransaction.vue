<script setup>
import { ref } from 'vue';
import {useToast} from 'vue-toastification'

const text = ref('')
const amount = ref(null)

const emit = defineEmits(['transactionSubmitted'])

const toast = useToast();

const onSubmit = () => {
    if(!text.value || !amount.value){
        toast.error('Both fields must be filled!');
        return;
    }

    const transactionData = {
        text: text.value,
        amount: parseFloat(amount.value)
    }

    emit('transactionSubmitted', transactionData)

    text.value = ''
    amount.value = ''
}
</script>

<template>
<h3>Yangi ma'lumot qo'shish</h3>        
<form id="form" @submit.prevent="onSubmit">
    <div class="form-control">
        <label for="text">Nomi</label>
        <input type="text" id="text" v-model="text" placeholder="Nomini kiriting..."/>
    </div>
    <div class="form-control">
        <label for="amount">
            Miqdori <br/>
            (minus belgisi bilan kiritilsa, chiqim hisoblanadi)
        </label>
        <input type="number" id="amount" v-model="amount" placeholder="Miqdorini kiriting..."/>
    </div>
    <button class="btn">Saqlash</button>
</form>
    
</template>