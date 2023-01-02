<script setup>
import MultiSelect from './components/MultiSelect.vue'
import {ref, onMounted} from 'vue';
import axios from 'axios';
const languages = ref([]);


onMounted(() => {
axios.get('http://localhost:3000/languages')
  .then((response) => {
    languages.value = response.data; 
  })
  .catch((error) => {
    console.log(error);
  });
})

 
</script>

<template>
<MultiSelect label="Select Programming Language" :data="languages" />
</template>

<style scoped>
 
</style>
