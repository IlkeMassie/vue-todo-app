<script setup lang="ts">

import { ref } from 'vue';
import deleteIcon from '../assets/delete.png'
import tagIcon from '../assets/price-tag.png'


type Category = {
    title: string, 
    color: string
}

const props = defineProps<({
    title: string,
    index: number,
    completed: boolean,
    categories: Category[],
    todoCategoryTitle: string | undefined,
    todoCategoryColor: string | undefined
})>()

const emit = defineEmits(['updateCategory', 'toggleCompleted', 'deleteTodo'])

const showCategorySelect = ref(false);

const selectedCategory = ref(props.categories.length ? props.categories[0].title : '');


function toggleCategorySelect(){
    showCategorySelect.value =!showCategorySelect.value;
}
function emitCategoryChange(){
    try {
       showCategorySelect.value = false; //to close the select list

        if(props.categories.length === 0){
            console.error('Categories array is empty')
            return
        }

        const selectedCategoryObject = props.categories.find(category => category.title === selectedCategory.value)

        if (selectedCategoryObject){          
            emit('updateCategory', {index: props.index, newCategory: selectedCategoryObject});
        } else {
            console.warn("No matching category found for ", selectedCategory.value)
        } 
    }
    catch (error){
        console.log('Error emitting category change: ', error)
    }
    
}


</script>

<template>
    <li>
        <div class="itemWrapper">
            <input 
                type="checkbox" 
                :checked="completed" 
                @change="$emit('toggleCompleted', index)"
            />
            {{title}}
        </div>
        <div>
            <span :style="{backgroundColor: todoCategoryColor}">{{todoCategoryTitle}}</span>
            <button @click="toggleCategorySelect">
                <img :src="tagIcon" alt="tag">
            </button>
            <select v-if="showCategorySelect" v-model="selectedCategory" @change="emitCategoryChange">
                <option v-for="category in categories" :key="category.title" :value="category.title">{{ category.title }}</option>
            </select>
            <button @click="$emit('deleteTodo', index)"><img :src="deleteIcon" alt="delete" /></button>
        </div>

    </li>

</template>


<style scoped>
.read-the-docs {
  color: #888;
}
li {
    background-color: #ebf0ef;
    padding: 5px;
    margin-top: 3px;
    display: flex;
    justify-content: space-between;
    border-radius: 25px;
    height: 25px;
}
img {
    width: 20px;
}
button {
    justify-content: right;
    border: none;
    cursor: pointer;
}
</style>
