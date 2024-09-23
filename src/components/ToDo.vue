<script setup lang="ts">

import { ref } from 'vue';
import TodoItem from './TodoItem.vue';
import CategoryItem from './CategoryItem.vue';
import AddTodoForm from './AddTodoForm.vue';


type Category ={
    title: string;
    color: string
}


type Todo = {
  title: string;
  completed: boolean;
  category: string;
};

const todos = ref<Todo[]>([{title: "Example", completed: false, category: ''}])
const categories = ref<Category[]>([{title: 'Urgent', color:"#CCC"}])

const newCategory = ref('');
const newCategoryColor = ref('');


//add a new to do
function addTodo(newTodo: string) {

    if(newTodo != "") {
        todos.value.push({title: newTodo, completed: false, category: ''})
    }
}

function addCategory(event: Event){
    event.preventDefault();

    if(newCategory.value != ""){
        categories.value.push({title: newCategory.value, color: newCategoryColor.value});
        console.log(categories.value[1])
        newCategory.value='';
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
    <div class="wrapper">
        <aside>
            <h3>Categories</h3>
            <ul>
                <CategoryItem v-for="(category, index) in categories"
                    :key="index"
                    :category="category.title"
                    :color="category.color">
                </CategoryItem>
            </ul>


            
            <form @submit="addCategory">
                <input type="color" class="color-picker" v-model="newCategoryColor">
                <input class="textField" type="text" v-model="newCategory">
                <button id="newCategory" class="button-1" type="submit">Add</button>
            </form>
        </aside>

        <main>
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
 
            <AddTodoForm
                @addTodo="addTodo">
            </AddTodoForm>

        </main>

        <section></section>

        <footer>
            <p><a href="https://www.flaticon.com/free-icons/delete" title="delete icons">Delete icons created by Google - Flaticon</a></p>
        </footer> 


   </div>
</template>


<style scoped>

.wrapper {
    display: grid;
    grid-template-columns: 0.8fr 2.2fr;
    min-height: 100vh;
    grid-template-rows: auto 100px;
  }

h1 {
    color: #ebf0ef;
}


.button-1 {
    margin-left: -50px;
}
#newTodo{
    background-color: #DB5461;
}

#newCategory{
    background-color: rgb(136, 136, 136);
}
input:focus{
    outline: none;
}

section {
    background-color: #98B6B1;
}

aside {
    background-color:#98B6B1;
    padding: 20px
}
ul {
    list-style: none;
    padding-inline-start: 0;
}
main ul {
    width: 450px;
}
main {
    margin-left: 40px;
}
footer {
    margin: 10px 20px 10px 40px;
    margin-top: auto;
}
footer p {
    text-align: right;
}
input {
    background-color: #ebf0ef;
}
a {
    text-decoration: none;
    color: black;
}


</style>
