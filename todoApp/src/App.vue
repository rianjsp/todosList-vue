<template>
  <div class="flex flex-col min-h-screen max-h-screen bg-slate-900 items-center justify-center">
    <h1 class="text-white box-border mb-11 font-semibold text-5xl border-b-4 rounded-mg first-letter:text-rose-500 first-letter:text-6xl  font-sans"><strong>Todos List</strong></h1>


    <!-- Header -->
    <div class="flex flex-row mb-6">
      <form @submit.prevent="addTask">
        <input v-model="todo" class=" py-2 px-2 rounded-xl text-center  inset-10 border-x-8 outline-offset-0 outline-none" type="text" placeholder="Insira sua task aqui...">
        <button type="submit" class=" active:scale-90 text-white py-2 px-2 ml-2 font-bold bg-sky-500 hover:bg-sky-700 rounded-xl w-16">+</button>
      </form>
    </div>
    
    
    <!-- Div central -->
    <div class="container box-border border-solid border-l-4 border-sky-200 mb-4 w-96 h-1/2 overflow-y-auto custom-scrollbar">

      <ul class="text-white font-semibold capitalize mt-5 m-5">
        <li class="flex flex-row justify-between items-center" v-for="task in todos" :key="task.id"> {{task.name}} <button class="ml-3 py-1 px-1 mx-1 my-1 bg-rose-500 rounded-xl w-9 h-6 justify-center  text-center items-center">-</button> </li>
      </ul>


    </div>

  </div>
</template>

<script setup >
import { ref, reactive} from 'vue';


// Ref sempre para tipos de dados primitivos
// Reactive para objetos...
const todo = ref('')
const todos = reactive([])


function addTask() {
  if (todo.value.trim() !== '') {
    todos.push({ name: todo.value, id: Math.floor(Math.random() * 1000) })
    todo.value = ''
    console.log(todos[0].name);
  } else { 
    alert('Erro')

  }
}
</script>

<style scoped>
/* Custom scrollbar styles for WebKit browsers (Chrome, Safari) */
.custom-scrollbar::-webkit-scrollbar {
  width: 12px;
}

.custom-scrollbar::-webkit-scrollbar-track {
  background: #2c2c2c; /* Track color */
  border-radius: 10px;
}

.custom-scrollbar::-webkit-scrollbar-thumb {
  background-color: #888; /* Thumb color */
  border-radius: 10px;
  border: 3px solid #2c2c2c; /* Space around thumb */
}

.custom-scrollbar::-webkit-scrollbar-thumb:hover {
  background-color: #555; /* Thumb color on hover */
}

/* Custom scrollbar styles for Firefox */
.custom-scrollbar {
  scrollbar-width: thin;
  scrollbar-color: #888 #2c2c2c; /* Thumb color and Track color */
}
</style>