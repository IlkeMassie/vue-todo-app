<script setup lang="ts">

defineProps({
    category: String,
    color: String
})


</script>


<template>
    <li>
        <span :style="{backgroundColor: color}">{{category}}</span>
    </li>

</template>   


<style>

</style>