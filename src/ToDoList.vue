<template>
  <button @click="showTimer = !showTimer" >Afficher / Masquer</button>
  <Timer v-if="showTimer"/>

  <Layout>

    <template v-slot:header> En tête</template>
    <template v-slot:aside> Sidebar</template>
    <template #main> Main</template>
    <template #footer> Footer</template>


  </Layout>
  <Button><strong>Demo</strong> de bouton</Button>

  <form action=" " @submit.prevent="addTodo">

    <fieldset role="group">
      <input v-model="newTodo" type="text"  placeholder="Tache à effectuer">
      <button :disabled="newTodo.length === 0 ">Ajouter</button>
    </fieldset>

  </form>

  <div v-if="todos.length === 0" > Vous n'avez pas de taches à faire :(</div>
  <div v-else>
    <ul>
      <li 
        v-for="todo in sortedTodos"
        :key ="todo.date"
        :class="{completed : todo.completed}"
        >
        <!--<label>
          <input type="checkbox" name="" v-model="todo.completed">
           {{todo.title}}
        </label>--> 
        <Checkbox :label="todo.title" 
          v-model="todo.completed"
        
        
      />
      </li>
    </ul>
     
    <label><input type="checkbox" v-model="hideCompleted"> Masquer les tâches complétées</label>

    <p v-if="remainningTodos > 0">
      {{ remainningTodos }} tâche{{ remainningTodos > 1 ? 's' : '' }} à faire
    </p>
  </div>

  <Checkbox label="Bonjour"/>

</template>

<script  setup>
import {ref, computed, onMounted} from 'vue'
import Checkbox from './components/Checkbox.vue';
import Button from './components/Button.vue';
import Layout from './components/Layout.vue';
import Timer from './components/Timer.vue';

const newTodo = ref('')
const hideCompleted = ref(false)
const todos = ref([
  // {
  //     title: 'Tâche de test',
  //     completed: true,
  //     date: 1,
  // },
  // {
  //     title: 'Tâche à faire',
  //     completed: false,
  //     date: 2,
  // }
])
const addTodo  = () => {
  todos.value.push(
    {
      title: newTodo.value,
      completed : false ,
      date : Date.now()

    }
  )
  
  newTodo.value = ''
 }

const sortedTodos = computed (() => {

  const sortedTodos = todos.value.toSorted((a,b)  => a.completed > b.completed ?  1 : -1)
    if (hideCompleted.value === true) {
      return sortedTodos.filter(t => t.completed === false )

    }
    return sortedTodos
  })

  const remainningTodos = computed(()  =>  {

    return todos.value.filter(t => t.completed === false).length
  })

const showTimer = ref(true)
  onMounted(() => {

    fetch('https://jsonplaceholder.typicode.com/todos')
    .then(r => r.json())
    .then(v => todos.value = v.map(todo => ({ ...todo,
       date: todo.id})))
  })

</script>

<style >   

.completed{

  opacity: .5 ;
  text-decoration: line-through;
}
</style>
