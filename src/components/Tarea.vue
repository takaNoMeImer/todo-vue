<script setup>
    import { ref } from 'vue';

    let tarea_actual = ""
    let tareas = ref([])

/*     function vaciarLocalStorage() {
        localStorage.removeItem('tareas')
        tareas.value = []
    } */
    function eliminarTweet(index) {
        tareas.value.splice(index, 1)

        localStorage.setItem('tareas', JSON.stringify(tareas.value))
    }

    function agregarTweetLocalStorage() {
        let setTareas
        setTareas = getTweetsLocalStorage()
        setTareas.push(tarea_actual)

        localStorage.setItem('tareas', JSON.stringify(setTareas))
        tarea_actual = ''
        // localStorage

        loadedTweets()
    }

    function getTweetsLocalStorage() {
        let getTareas

        if (localStorage.getItem("tareas") === null) {
            getTareas = []
        } else {
            getTareas = JSON.parse(localStorage.getItem("tareas"))
        }
        return getTareas
    }

    const loadedTweets = () => {
        tareas.value = getTweetsLocalStorage()
    }
    loadedTweets()
</script>
<template>
    <div class="container">
        <div class="task-input">
            <input type="text" placeholder="Agregar tarea" v-model="tarea_actual" v-on:keypress.enter="agregarTweetLocalStorage">
        </div>

        <div class="list-task">
            <div class="tarea">
                <p v-if=" tareas.length === 0 ">No hay tareas para mostrar</p>
                <p v-for=" task,index in tareas" key="task">
                    <img src="../assets/check_empty.svg" alt="">
                    <p>{{task}}</p>
                    <img src="../assets/delete.svg" alt="" @click="eliminarTweet(index)" />
                </p>
            </div>
        </div>
    </div>
</template>
<style>
    .container {
        width: 90%;
        margin: 2rem auto;
    }
    .task-input {
        width: 70%;
        border: 1px solid white;
        border-radius: 5px;
        margin: 0 auto;
        display: flex;
    }
    .task-input input {
        border: none;
        outline: none;
        padding: 10px;
        width: 100%;
        display: block;
        background-color: white;
        color: black;
        font-family: 'Poppins', sans-serif;
        font-size: 1.5rem;
    }
    .task-input img {
        width: 50px;
        padding: 5px;
        background-color: white;
    }
    .list-task {
        width: 70%;
        background-color: white;
        margin: 2rem auto;
        border-radius: 5px;
    }
    .tarea {
        padding: 10px;
        font-family: 'Poppins', sans-serif;
    }
    .tarea p {
        display: flex;
        align-items: center;
        font-size: 1.4rem;
        justify-content: space-between;
        padding: 8px;
    }
    .tarea img {
        width: 30px;
    }
    @media (max-width: 768px) {
        .container {
            width: 95%;
        }
        .task-input, .list-task {
            width: 80%;
        }
    }
    @media (max-width: 500px) {
        .container {
            width: 98%;
        }
        .task-input {
            width: 90%;
        }
        .task-input input {
            font-size: 1rem;
        }
        .list-task {
            width: 90%;
        }
        .tarea p {
            font-size: 1rem;
        }
        .tarea img {
            width: 20px;
        }
    }
</style>