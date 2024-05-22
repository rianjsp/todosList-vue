<template>
  <div class="appcontent flex flex-col min-h-screen max-h-screen bg-slate-900 items-center justify-center">
    <!-- Preloader -->
    <Preloader/>
    
    <h1 class="text-white box-border mb-11 font-semibold text-5xl border-b-4 rounded-mg first-letter:text-rose-500 first-letter:text-6xl  font-sans"><strong>Todos List</strong></h1>


    <!-- Header -->
    <div class="flex flex-row mb-6">
      <form @submit.prevent="addTask" class="justify-center items-center flex flex-row">
        <input id="ipt_todo" v-model="todo" class=" py-2 px-2 rounded-xl text-center  inset-10 border-x-8 outline-offset-0 outline-none" type="text" placeholder="Insira sua task aqui..." required maxlength="60">
        <button type="submit" class=" active:scale-90 text-white py-2 px-2 ml-2 font-bold bg-sky-500 hover:bg-sky-700 rounded-xl">
          <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor" class="w-6 h-6">
              <path fill-rule="evenodd" d="M12 3.75a.75.75 0 0 1 .75.75v6.75h6.75a.75.75 0 0 1 0 1.5h-6.75v6.75a.75.75 0 0 1-1.5 0v-6.75H4.5a.75.75 0 0 1 0-1.5h6.75V4.5a.75.75 0 0 1 .75-.75Z" clip-rule="evenodd" />

          </svg>
        </button>
      </form>
    </div>
    
    
    <!-- Div central -->
    <div class="container box-border border-solid border-l-4 border-sky-200 mb-4 w-96 h-1/2 overflow-y-auto custom-scrollbar">

      <ul class="text-white font-semibold capitalize mt-5 m-5">
        <li class="flex flex-row justify-between items-center mb-6" v-for="task in todos" :key="task.id"> 
          

          <strong>{{task.name}} </strong>

          <button class="ml-3 py-1 px-1 mx-1 my-1 bg-rose-500 rounded-xl  justify-center  text-center items-center active:scale-90 hover:bg-rose-800 text-white">
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor" class="w-6 h-6">
  <path fill-rule="evenodd" d="M5.47 5.47a.75.75 0 0 1 1.06 0L12 10.94l5.47-5.47a.75.75 0 1 1 1.06 1.06L13.06 12l5.47 5.47a.75.75 0 1 1-1.06 1.06L12 13.06l-5.47 5.47a.75.75 0 0 1-1.06-1.06L10.94 12 5.47 6.53a.75.75 0 0 1 0-1.06Z" clip-rule="evenodd" />
</svg>

          </button> 
        </li>
      </ul>


    </div>

  </div>
</template>

<script setup >
import { ref, reactive} from 'vue';
import Preloader from '../components/Preloader.vue';

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


/*Custom scrollbar o codigo foi copiado da internet*/
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

#ipt_todo::placeholder{
  font-weight: 600;
}
</style>