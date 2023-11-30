<template>
    <h4>My Balance</h4>
    <h1 id="balance">${{ total }}</h1>
</template>

<script setup>

const props = defineProps({
    total: {
        type: Number,
        required: true,
    }
})
</script>


<style>
h4{
    font-size: 15px;
    font-weight: 400;
    margin-bottom: 5px;
}

h1{
    color: #0FB834;
    font-size: 25px;
    margin-bottom: 15px;
}
</style>
