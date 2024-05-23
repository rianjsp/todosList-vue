<template>
  <div v-if="showPreloader" id="preloader" class="fixed inset-0 flex flex-col justify-center bg-white items-center">
    <span class="loader"></span>
  </div>
  <div v-show="!showPreloader" id="appcontent">
    
  </div>

</template>

<script setup>
import { ref, onMounted } from 'vue';

const showPreloader = ref(true);

onMounted(() => {
  setTimeout(() => {
    showPreloader.value = false;
  }, 1000);
});
</script>

<style scoped>
#preloader {
  background: #ffffff;
}

.loader {
  border: 4px solid rgba(0, 0, 0, 0.1);
  border-left-color: #e64646;
  border-radius: 50%;
  width: 50px;
  height: 50px; 
  animation: spin 1s linear infinite;
}


@keyframes spin {
  to {
    transform: rotate(360deg);
  }
}
</style>
