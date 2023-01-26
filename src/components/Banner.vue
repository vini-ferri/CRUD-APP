<template>
    <div id="main-banner">
        <p>Cadastro de pessoas, de uma maneira simples.</p>
    </div>
</template>

<script>
    export default {
        name: "Banner"
    }
</script>

<style scoped>

    #main-banner {
        height: 500px;
        display: flex;
        align-items: center;
        justify-content: flex-start;
        background-image: url('../assets/notebook.jpg');
        background-attachment: fixed;
        background-position: center;
        background-repeat: no-repeat;
        background-size: 105%;
    }

    #main-banner p {
        color: #fff;
        font-size: 40px;
        margin-left: 5%;
    }

</style>