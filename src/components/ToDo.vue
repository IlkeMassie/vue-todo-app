<script setup lang="ts">

import { ref } from 'vue';
import TodoItem from './TodoItem.vue';



type Todo = {
  title: string;
  completed: boolean;
};

const todos = ref<Todo[]>([])

const newTodo = ref('');

function addTodo(event: Event) {
    event.preventDefault();

    if(newTodo.value != "") {
        todos.value.push({title: newTodo.value, completed: false})
        newTodo.value='';
    }
}

//delete 1 item starting from the index passed from child component 'TodoItem'
function deleteTodo(index: number){
    todos.value.splice(index, 1);
}

//toggle completed. When the checkbox state is changed, modify the boolean value to the opposite value.
function toggleCompleted(index: number){
    todos.value[index].completed  = !todos.value[index].completed;
}

</script>

<template>
    <h1>To Do List</h1>
    <ul>
        <TodoItem v-for="(item, index) in todos" 
            :key="index" 
            :title="item.title" 
            :index="index"
            :completed="item.completed"
            @deleteTodo="deleteTodo"
            @toggleCompleted="toggleCompleted">
        </TodoItem>

    </ul>

    <form @submit="addTodo">
        <input type="text" v-model="newTodo">
        <button type="submit">New todo</button>
    </form>

</template>


<style scoped>
.read-the-docs {
  color: #888;
}
</style>
