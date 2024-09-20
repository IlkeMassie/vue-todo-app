<script setup lang="ts">


defineProps({
    title: String,
    index: Number,
    completed: Boolean
})

</script>

<template>
    <li>
        <input 
            type="checkbox" 
            :checked="completed" 
            @change="$emit('toggleCompleted', index)"
        />
        {{title}}
        <button @click="$emit('deleteTodo', index)">deleteToDo</button>
    </li>

</template>


<style scoped>
.read-the-docs {
  color: #888;
}
</style>
