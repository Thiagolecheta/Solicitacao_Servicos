<template>
    <div class="mensagem-container" >
        <p>{{ msg }}</p>
    </div>
</template>

<script>

export default {
    name: 'Mensage',
    props: {
        msg: String
    }
}
</script>

<style scoped>
    .mensagem-container{
        display: flex;
        align-items: center;
        justify-content: flex-start;
        width: 400px;
        margin: 0 auto;
        font-size: 16px;
        background-color: #CCE5FF;
        color: #004085;
        border: 2px solid #B8DAFF;
        border-radius: 5px;
        margin-bottom: 20px;
        padding: 10px;
    }
</style>
