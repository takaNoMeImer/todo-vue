<script setup>

</script>
<template>
    <header>
        <div class="nav">
            <img src="../assets/vue.svg" alt="">
            <p class="max
            ">Aplicacion de Tareas</p>
            <p class="min">Tareas</p>
        </div>
    </header>
</template>
<style>
    header {
        /* background-color: rgb(47, 47, 66); */
        background-color: rgb(247, 245, 245);
        padding: 14px;
    }
    .nav {
        width: 90%;
        margin: 0 auto;
        display: flex;
        align-items: center;
        column-gap: 2rem;
    }
    .nav p {
        font-size: 1.5rem;
        font-family: 'Poppins', sans-serif;
    }
    .min { display: none; }
    @media (max-width: 500px) {
        .min { display: block;}
        .max { display: none; }
    }
</style>