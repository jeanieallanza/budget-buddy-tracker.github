<template>
    <h3>History</h3>
    <hr class="line">
    <ul id="list" class="list">

        <div
            v-for="transaction in transactions"
            :key="transaction.id"
            :class="transaction.amount < 0 ? 'minus' : 'plus'"
        >
            <li class="transaction"> 
                <span> {{ transaction.text }}</span>
                <span class="amount">${{ transaction.amount }}</span>
            </li>
            <li>
                <button @click="deleteTransaction(transaction.id)" class="delete-btn">
                <i class='bx bxs-trash'></i>
                </button>
            </li>
        </div>
    </ul>
</template>

<script setup>

const emit = defineEmits(['transactionDeleted'])

const props = defineProps({
    transactions: {
        type: Array,
        required: true,
    }
});

const deleteTransaction = (id) => {
    emit('transactionDeleted', id);
}
</script>

<style>
h3 {
    font-size: 15px;
    margin-bottom: 5px;
}

.line {
    background: #fff;
    height: 1px;
    margin-bottom: 10px;
}

.list {
    display: flex;
    flex-direction: column;
}

.list div {
    display: flex;
    align-items: center;
    justify-content: space-between;
}

.list li {
    color: #fff;
    list-style: none;
    margin-bottom: 5px;
    margin-top: 2px;
}

.transaction {
    display: flex;
    align-items: flex-start;
    justify-content: space-between;
    padding: 10px;
    background: #fff;
    width: 90%;
    margin-right: 10px;
    border-radius: 10px;
}

.list li span {
    color: #222;
    font-weight: 700;
    font-size: 15px;
}

.list li span.amount {
    color: #0FB834;
}

button {
    padding: 10px;
    background: #fff;
    border-radius: 10px;
    transition: 0.3s;
}

button:hover{
    background: #f0ebeb;
}

button i {
    color: #C5180D;
    font-size: 18px;
    transition: transform 0.3s ease-in-out;
}

button i:hover{
    transform: scale(1.2); 
}
</style>
