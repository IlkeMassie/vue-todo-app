<script setup lang="ts">

import deleteIcon from '../assets/delete.png'

defineProps({
    title: String,
    index: Number,
    completed: Boolean
})

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

        <button @click="$emit('deleteTodo', index)"><img :src="deleteIcon" alt="delete" /></button>
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
