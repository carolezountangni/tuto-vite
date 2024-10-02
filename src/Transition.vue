<template>
    <button @click="toggleSpoiler"> Afficher / Masquer le spoiler</button>

    <Transition>
        <div class="spoiler" v-if="showSpoiler">

        A la fin de la série Marc Cunningan meurt !
    </div>
    </Transition>

</template>
   
<script setup>
import {computed , ref } from 'vue';

const showSpoiler = ref(false)
const toggleSpoiler = () => showSpoiler.value = !showSpoiler.value



</script>
<style>
.spoiler{
    padding : 1rem;
    border : 1px solid cyan;
    transition: .5s;
}

.v-enter-from {

    opacity: 0;
    transform: translateX(10px);
}
.v-leave-to{
    opacity: 0;
    transform: translateX(-10px);
}
</style>