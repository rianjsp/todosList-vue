<template>
  <div class="flex flex-col min-h-screen bg-slate-900 items-center justify-center">
    <h1 class="text-white box-border absolute top-80 font-semibold text-5xl border-b-4 rounded-mg first-letter:text-rose-500 first-letter:text-6xl  font-sans"><strong>Todos List</strong></h1>


    <!-- Header -->
    <div class="flex flex-row">
      <form @submit.prevent="addTask">
        <input v-model="todo" class=" py-2 px-2 rounded-xl text-center  inset-10 border-x-8 outline-offset-0 outline-none" type="text" placeholder="Insira sua task aqui...">
        <button type="submit" class=" active:scale-90 text-white py-2 px-2 ml-2 font-bold bg-sky-500 hover:bg-sky-700 rounded-xl w-16">+</button>
      </form>
    </div>
    
    
    <!-- Div central -->
    <div class="container box-border border-solid border-x-4 border-sky-200 w-96 h-96">

      


    </div>

  </div>
</template>

<script setup >
import { ref } from 'vue';


// Ref sempre para tipos de dados primitivos
const todo = ref('')
const todos = ref([])


function addTask() {
  console.log("addTask");
}

</script>

<style scoped>

</style>