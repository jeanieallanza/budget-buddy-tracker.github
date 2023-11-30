<template>
  <div class="container">
   <div class="insidebox">
    <Header/>
    <Balance :total="total"/>
    <IncomeExpenses :income="+income" :expenses="+expenses"/>
    <TransactionList 
      :transactions="transactions" 
      @transactionDeleted="handleTransactionDeleted"
      />
    <AddTransaction 
    @transactionSubmitted="handleTransactionSubmitted"
    />
   </div>
  </div>
</template>

<script setup>
import Header from './components/Header.vue';
import Balance from './components/Balance.vue';
import IncomeExpenses from './components/IncomeExpense.vue';
import TransactionList from './components/TransactionList.vue';
import AddTransaction from './components/AddTransaction.vue';

import { ref, computed, onMounted } from 'vue';

import { useToast } from 'vue-toastification'

const toast = useToast();
const transactions = ref([]);

onMounted(() => {
  const saveTransactions = JSON.parse(localStorage.getItem('transactions'));

  if (saveTransactions) {
    transactions.value = saveTransactions;
  }
});

// For the Total amount
const total = computed(() => {
  return transactions.value.reduce((acc, transaction) => {
    return acc + transaction.amount;
  }, 0);
});

// For the Total Income
const income = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount > 0)
    .reduce((acc, transaction) => {
    return acc + transaction.amount;
    }, 0)
    .toFixed(2);
});

// For the Total Expenses
const expenses = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount < 0)
    .reduce((acc, transaction) => {
    return acc + transaction.amount;
    }, 0)
    .toFixed(2);
});

// Handle Transaction Submitted
const handleTransactionSubmitted = (transactiondata) => {
  transactions.value.push({
    id: generateUniqueId(),
    text: transactiondata.text,
    amount: transactiondata.amount
  });

  saveTransactionsToLocalStorage();

  toast.success('Transaction added');
};

// Id Generated
const generateUniqueId = () => {
  return Math.floor(Math.random() * 1000000);
};

// Delete Transaction 
const handleTransactionDeleted = (id) => {
  transactions.value = transactions.value.filter((transaction) =>
    transaction.id !== id
  );

  saveTransactionsToLocalStorage();

  toast.success('transaction deleted');
};

// Save to LocalStorage
const saveTransactionsToLocalStorage = () => {
  localStorage.setItem('transactions', JSON.stringify(transactions.value));
}
</script>
