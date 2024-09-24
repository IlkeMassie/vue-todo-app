<script setup lang="ts">
import { ref } from 'vue';


const emit = defineEmits(['addCategory'])

const newCategory = ref('');
const newCategoryColor = ref('');

function addCategory(){
    if(newCategory.value.trim()){
        emit('addCategory', newCategory.value, newCategoryColor.value)
        newCategory.value = "";
        newCategoryColor. value = "";
    }
}

</script>



<template>
    <form @submit.prevent="addCategory">
        <input type="color" class="color-picker" v-model="newCategoryColor">
        <input class="textField" type="text" v-model="newCategory">
        <button id="newCategoryBtn" class="button-1" type="submit">Add</button>
    </form>
</template>




<style scoped>
#newCategoryBtn{
    background-color: rgb(136, 136, 136);
}
</style>