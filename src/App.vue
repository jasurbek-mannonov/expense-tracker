<script>
import Header from './components/Header.vue';
import Balance from './components/Balance.vue'
import IncomeExpense from './components/IncomeExpense.vue';
export default{
  components: {
    Header,
    Balance,
    IncomeExpense
}
}
</script>

<template>
  <Header/>
  <div class="container">
    <Balance/>
    <IncomeExpense/>
  </div>
</template>