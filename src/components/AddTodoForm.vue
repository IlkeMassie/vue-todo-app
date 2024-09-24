<script setup lang="ts">
import { ref } from 'vue';


const newTodo = ref('');


const emit = defineEmits(['addTodo'])


const addTodo = () => {
  if (newTodo.value.trim()) {
    // Emit the 'addTodo' event to the parent with the newTodo value
    emit('addTodo', newTodo.value);
    // Clear the input field after adding a new todo
    newTodo.value = '';
  }
};
</script>


<template>
    <form @submit.prevent="addTodo">
        <input class="textField" type="text" v-model="newTodo">
        <button id="newTodoBtn" class="button-1" type="submit">New todo</button>
    </form>
</template>

<style scoped>


#newTodoBtn{
    background-color: #DB5461;
}

</style>