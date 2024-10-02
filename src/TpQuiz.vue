<template>
    <div class="container">
        <h1>TP QUIZ</h1>

        <div v-if="state === 'error'">
            <p>Impossible de charger le quiz</p>
        </div>

        <div :aria-busy="state === 'loading'">
            <Quiz :quiz="quiz" v-if="quiz"/>
        </div>

    </div>
</template>



<script setup>

import { onMounted, ref } from 'vue';
import Quiz  from './components/Quiz.vue';

const quiz = ref(null)
const state = ref('loading')

onMounted(() => {

    fetch('/quiz.json')
    .then(r => {
        if(r.ok){
            return r.json()
        } 
        throw new Error ('Impossible de récupérer le  json')

    }) 
    .then(data => {
        quiz.value = data
        state.value = 'idle'
    })
    .catch(e => {
        state.value = 'error'
    })

})


</script>


<style>

h1 { 
    color: black;
    background-color:aliceblue;
    text-align: end;
    
    }
.container{

    margin-top: 2rem;
}
</style>