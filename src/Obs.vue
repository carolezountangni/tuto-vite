<template>

    <input type="text" name="" id="" v-model="page.title">

    Temps écoulé : {{ time }}
    <button @click="reset"> Reset </button>

</template>

<script setup>

import { ref, watch, watchEffect} from 'vue'
import { useTimer } from './composable/useTimer';

const {time, reset} = useTimer()
const page = ref({
    title: ''
})
// Dériver une valeur à partie=r d'une autre valeur reactive 
watch(() => page.value.title, (newValue, oldValue) => {

    document.title = newValue
}
// // Executer au chargement de la page 
// , {immediate :true}

)
// Effet de bord en dehors du cadre de vuejs
watchEffect(() => {
    document.title = page.value.title
})



</script>