<template>
  <div class="appcontent bg-slate-900 flex flex-col min-h-screen max-h-screen items-center justify-center">

    <!-- Preloader -->
    <Preloader/>
    
    <!-- Campo para sociais e Titulo do app -->
    <div class="flex flex-col mt-2">
    <Socials />
    <h1 class="text-white box-border mb-6 font-semibold text-5xl border-b-4 rounded-mg first-letter:text-rose-500 first-letter:text-6xl  font-sans"><strong>To<span class="text-rose-500">-</span>do List</strong></h1>
    </div>


    <!-- Cabeça do form para input de tasks -->
    <div class="flex flex-row mb-6">

        <!-- Form input -->
      <form @submit.prevent="addTask" class="justify-center items-center flex flex-row">
        <input id="ipt_todo" v-model="todo" class=" py-2 px-2 rounded-xl text-center  inset-10 border-x-8 outline-offset-0 outline-none" type="text" placeholder="Insira sua task aqui..." required maxlength="60">
        <select v-model="selectOption" id="selectOpt" class="py-2 px-2 rounded-xl mx-2 font-semibold">
            <option value="green" selected>Normal</option>
            <option value="white" >Media</option>
            <option value="red" >Urgente</option>
        </select>

        <!-- Botao com svg de icones do site HEROICONS -->
        <button type="submit" class=" active:scale-90 text-white py-2 px-2 ml-2 font-bold bg-sky-500 hover:bg-sky-700 rounded-xl">
          <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor" class="w-6 h-6">
              <path fill-rule="evenodd" d="M12 3.75a.75.75 0 0 1 .75.75v6.75h6.75a.75.75 0 0 1 0 1.5h-6.75v6.75a.75.75 0 0 1-1.5 0v-6.75H4.5a.75.75 0 0 1 0-1.5h6.75V4.5a.75.75 0 0 1 .75-.75Z" clip-rule="evenodd" />

          </svg>
        </button>
      </form>
    </div>
    
    
    <!-- Div central -->
    <div class="container box-border border-solid border-l-4 border-rose-500 mb-4 h-3/4 overflow-y-auto overflow-x-auto custom-scrollbar">

        <!-- Começo dos itens dinamicos -->
      <ul class="text-white font-semibold capitalize mt-5 m-5 box-border flex flex-col flex-wrap">
        <li class="flex flex-row bg-slate-950 m-4 py-5 px-7 rounded-lg backdrop-opacity-10 justify-between items-center mb-6" v-for="task in todos" :key="task.id"> 
            
            <!-- Nome da task e Strike na task-->
            <div class="flex flex-row">
                <input class="mr-2 w-6 h-6 cursor-pointer" type="checkbox" id="checked" v-model="task.completed">
                <strong :class="{ 'line-through': task.completed }">{{task.name}}</strong>  
            </div>

            <!-- Tag de urgencia e restante da div-->
            <div class="flex flex-row justify-center items-center ml-8">
                <div class="flex flex-row justify-between" :style="{ borderRadius: '20px',width: '20px', borderBottomColor: task.urgency, borderBottomWidth: '10px', borderBottomStyle: 'solid' }">
                 
                </div>
                <button @click="removeTask(task.id)" class="ml-3 py-1 px-1 mx-1 my-1 bg-rose-500 rounded-xl  justify-center  text-center items-center active:scale-90 hover:bg-rose-800 text-white">
                    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor" class="w-6 h-6">
                    <path fill-rule="evenodd" d="M5.47 5.47a.75.75 0 0 1 1.06 0L12 10.94l5.47-5.47a.75.75 0 1 1 1.06 1.06L13.06 12l5.47 5.47a.75.75 0 1 1-1.06 1.06L12 13.06l-5.47 5.47a.75.75 0 0 1-1.06-1.06L10.94 12 5.47 6.53a.75.75 0 0 1 0-1.06Z" clip-rule="evenodd" />
                    </svg>
                </button> 
            </div>
        
        </li>
      </ul>
            
        
    </div>
    
  </div>
</template>

<script setup >
import { ref, reactive} from 'vue';
import Preloader from '../components/Preloader.vue';
import Socials from '../components/Socials.vue'

// Ref sempre para tipos de dados primitivos, Reactive para objetos...

const todo = ref('');
const todos = reactive([]);
const selectOption = ref('white');
const completeded = ref(false);

// Função para adicionar task
function addTask() {
  if (todo.value.trim() !== '') {
    todos.push({ name: todo.value, id: Math.floor(Math.random() * 1000), urgency: selectOption.value, completeded: false });
    todo.value = '';
    selectOption.value = 'white';
  } else {
    alert('Adicione pelomenos um nome para a task!');
  }
}

// Função de remoção da task
function removeTask(id) {
  const index = todos.findIndex(task => task.id === id);
  if (index !== -1) {
    todos.splice(index, 1);
  }
}


</script>

<style >


/*Custom scrollbar o codigo foi copiado da internet*/
.custom-scrollbar::-webkit-scrollbar {
  width: 12px;
}

.custom-scrollbar::-webkit-scrollbar-track {
  background: #2c2c2c; 
  border-radius: 10px;
}

.custom-scrollbar::-webkit-scrollbar-thumb {
  background-color: #888;
  border-radius: 10px;
  border: 3px solid #2c2c2c; 
}

.custom-scrollbar::-webkit-scrollbar-thumb:hover {
  background-color: #555; 
}

.custom-scrollbar {
  scrollbar-width: thin;
  scrollbar-color: #888 #2c2c2c; 
}

#ipt_todo::placeholder{
  font-weight: 600;
}
</style>