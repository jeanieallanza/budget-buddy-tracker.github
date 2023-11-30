<template>
   <h3>Add new transaction</h3>
   <hr class="line">
   <form id="form" @submit.prevent="onSubmit">
    <div class="form-control">
        <label for="text">Text</label>
        <input
            type="text" 
            id="text" 
            placeholder="Enter text..."
            v-model="text"
        >
    </div>

    <div class="form-control">
        <label
         for="amount">Amount
         <br>
            (negative - expense, positive - income)
        </label>

        <input 
            type="text"
            id="amount"
            placeholder="Enter amount..."
            v-model="amount"
        >
    </div>

    <button class="btn">Add new transaction</button>
   </form>
</template>

<script setup>
import { ref } from 'vue';
import { useToast } from 'vue-toastification'

const text = ref('');
const amount = ref('');
const toast = useToast();

const emit = defineEmits(['transactionSubmitted']);

const onSubmit = () => {
    if (!text.value || !amount.value) {
        toast.error('Both fields must be filled');
        return;
    }

    const transactiondata = {
        text: text.value,
        amount: parseFloat(amount.value)
    }

    emit('transactionSubmitted', transactiondata);

    text.value = '';
    amount.value = '';
};
</script>

<style scoped>
h3 {
    margin-top: 10px;
}

.line {
    background: #fff;
    height: 1px;
    margin-bottom: 10px;
}

form {
    margin-top: 10px;
}

.form-control {
    display: flex;
    flex-direction: column;
    margin-top: 10px;
}

.form-control label {
    color: #fff;
    margin-bottom: 5px;
    font-size: 15px;
}

input {
    padding: 10px;
    border-radius: 10px;
    outline: none;
}

button {
    border-radius: 10px;
    background: #270FB8;
    color: #fff;
    width: 50%;
    border: none;
    margin-top: 15px;
}
</style>
