<template>
    <div class="inc-exp-container">
        <div class="box">
            <h4>Income</h4>
            <p id="money-plus" class="money plus">+${{ income }}</p>
        </div>

        <div class="box">
            <h4>Expense</h4>
            <p id="money-minus" class="money minus">${{ expenses }}</p>
        </div>
    </div>
</template>

<script setup>

const props = defineProps({
    income: {
        type: Number,
        required: true,
    },
    expenses: {
        type: Number,
        required: true,
    },
});
</script>


<style>
.inc-exp-container {
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 0 75px;
    margin-bottom: 15px;
}

.box {
    border-radius: 10px;
    border: 1px solid rgba(0, 0, 0, 0.25);
    background: #FFF;
    width: 300px;
    margin: 0 5px;
    padding: 10px 40px;
}

.box h4 {
    color: #222;
    font-weight: 700;
    font-size: 15px;
}

.box .money {
    font-size: 18px;
    font-weight: 400;
}

.box .plus {
    color: #0FB834;
}

.box .minus {
    color: #C5180D;
}
</style>
