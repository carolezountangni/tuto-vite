

<template>
<!--  code html qui sera rendu -->
  <h1>Bonjour {{ firstName.toUpperCase()}}   </h1>
 <!--injecter et interpreter  du code html malgré la protection qui le protège en haut--> 
  <div v-html="firstName"></div>
  <p>Comment allez vous ? </p>

  <!-- utiliser un atribut dynamique ici dans la variable id  -->

  <p v-bind:id="count"> Compteur : {{ count }}</p>
  <p :id="`p-${count}`" :class="{active : count > 5}"> Compteur p-id : {{ count }}</p>

  <!--afficher et masquer un élement -->
  <div class="" v-show="count >= 5"> Bravo vous avez cliqué plus de 5 fois </div>
  <!--inverse  du v-show-->
    <div class="" v-hide="count >= 5"> Bravo vous avez cliqué plus de 5 fois </div>

  <!--supprimer un element du Dom  7:51-->

  <div class="" v-if="count >= 5"> Bravo vous avez cliqué plus de 5 fois </div>
  <div class="" v-else="count <= 5"> Bravo vous avez cliqué moins de 5 fois </div>

  <button v-on:click="increment">Incrémenter</button><br/><br/>
  <button @click="decrement">Decrémenter</button>
<hr>

  <p :style="{color: count2 > 5 ? 'red' : 'green'}"> Compteur 2 : {{ count2 }}</p>
    <button @click="count2++">Incrémenter2</button><br/><br/>
    <button @click="count2--">Decrémenter2</button><br/><br/>


<hr>
    <!--Utiliser v-for pour for et toujours  avec key  pur conserver les elements et non les récreéer -->

   
    <button @click="sortMovies">Réorganiser</button><br/><br/>

     <form action="" @submit.prevent="addMovie">
      <input type="text" placeholder="Nouveau Film" v-model="movieName ">
      <button>Ajouter</button>
    </form>
    <ul>
      <li v-for="movie in movies" :key="movie">

        {{ movie }} <button @click="deleteMovie(movie)">Supprimer</button>
      </li>
    </ul>

<hr>

<ul>
  <li>{{ person.firstname }}</li>
  <li>{{ person.lastname }}</li>
  <li>{{ person.age }}</li>
</ul>
<button type="button" @click.prevent="randomAge"> Changer age </button>


</template>

<script  setup>
import {ref} from 'vue'
// Ecrire du javascript
const firstName = '<span>John</span>'
const count = ref(0)
const count2 = ref(0)
const movieName = ref('')
const movies = ref([
  'Matrix',
  'Lilo & Stitch',
  'Titanic'
])
const person = ref({
   firstname : 'John',
   lastname : 'Doe',
   age : 20
})


const increment = () => {
  count.value++
}

const decrement = (event) => {
  console.log(event) 
  count.value--
}

setInterval(() =>{
  count2.value++
}, 1000);

const deleteMovie = (movie) => {

  movies.value = movies.value.filter(m => m !== movie)

}
const sortMovies = () => {
  movies.value.sort((a,b) => a > b ? 1 : -1 )
}

const addMovie = (event) => { 

  // event.preventDefault()
  movies.value.push(movieName.value)
  movieName.value = ''
}
const randomAge = () => {

  person.value.age = Math.round(Math.random() *100)


}

</script>

<style >
/* css  pour me style */

h1{

  color: red;
}


button {
    margin: 15px 25px; /* Espacement intérieur du bouton */
    font-size: 16px; /* Taille de la police */
    border: none; /* Pas de bordure */
   
}
.active{ color: red;} 


</style>
