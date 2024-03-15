<script setup>
import Header from "./components/Header.vue";
import Balance from "./components/Balance.vue";
import IncomeExpenses from "./components/IncomeExpenses.vue";
import TransactionList from "./components/TransactionList.vue";
import AddTransaction from "./components/AddTransaction.vue";
import { useToast } from "vue-toastification";
//////////composition api/////////////
import { ref, computed } from "vue";
const transactions = ref([]);
//// get total
const total = computed(() => {
  return transactions.value
    .reduce((acc, transaction) => {
      return acc + transaction.amount;
    }, 0)
    .toFixed(2);
});

//// get income
const income = computed(() => {
  return transactions.value
    .filter((f) => f.amount > 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount;
    }, 0)
    .toFixed(2);
});

//// get expenses
const expenses = computed(() => {
  return transactions.value
    .filter((f) => f.amount < 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount;
    }, 0);
});
const toast = useToast();
// Add transaction
const handleTransactionSubmitted = (transactionData) => {
  transactions.value.push({
    id: Math.floor(Math.random() * 100),
    ...transactionData,
  });
  toast.success("Transaction added");
};

// delete transaction
const handleTransactionDeleted = (id) => {
  transactions.value = transactions.value.filter((obj) => obj.id !== id);

  toast.success("Transaction deleted");
};
</script>

<template>
  <Header />
  <div class="container">
    <Balance :total="total" />
    <IncomeExpenses :income="+income" :expenses="+expenses" />
    <TransactionList
      :transactions="transactions"
      @transactionDeleted="handleTransactionDeleted"
    />
    <AddTransaction @transactionSubmitted="handleTransactionSubmitted" />
  </div>
</template>
