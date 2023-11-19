<script setup>
import Header from './components/Header.vue';
import Balance from './components/Balance.vue'
import IncomeExpense from './components/IncomeExpense.vue';
import TransactionList from './components/TransactionList.vue';
import AddTransaction from './components/AddTransaction.vue';

import { useToast } from 'vue-toastification';

import { ref, computed, onMounted } from 'vue';

const toast = useToast()

const transactions = ref([])

onMounted(() => {
  const savedTransactions = JSON.parse(localStorage.getItem('transactions'));

  if(savedTransactions){
    transactions.value = savedTransactions
  }
})

// Get total
const total = computed(() => {
  return transactions.value.reduce((acc, transaction) => {
    return acc + transaction.amount
  }, 0 )
})

// Get income
const income = computed(() => {
  return transactions.value
  .filter((transaction) => transaction.amount > 0)
  .reduce((acc, transaction) => {
    return acc + transaction.amount
  }, 0 ).toFixed(2)
})

// Get expence
const expense = computed(() => {
  return transactions.value
  .filter((transaction) => transaction.amount < 0)
  .reduce((acc, transaction) => {
    return acc + transaction.amount
  }, 0 ).toFixed(2)
})

// Add transaction
const handleTransactionSubmitted = (transactionData) => {
  transactions.value.push({
    id: generUniqueId(),
    text: transactionData.text,
    amount: transactionData.amount
  })

  saveTransactionsToLocalStorage()
  toast.success('Ma\'lumot qo\'shildi')
}

// Generate uniue ID
const generUniqueId = () => {
  return Math.floor(Math.random() * 1000000)
}

// Delete transaction
const handleTransactionDeleted = (id) => {
  transactions.value = transactions.value.filter((transaction) => transaction.id !== id)

  saveTransactionsToLocalStorage()
  toast.success('Ma\'lumot o\'chirildi')
}

// Save to localstorage
const saveTransactionsToLocalStorage = () => {
  localStorage.setItem('transactions', JSON.stringify(transactions.value))
}

</script>

<template>
  <div style="margin: 15px;">
    <Header/>
    <div class="container">
      <Balance :total="total"/>
      <IncomeExpense :income="+income" :expense="+expense"/>
      <TransactionList :transactions="transactions" @transactionDeleted="handleTransactionDeleted"/>
      <AddTransaction @transactionSubmitted="handleTransactionSubmitted"/>
    </div>
  </div>
</template>