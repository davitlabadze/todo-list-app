
<template>
    <header>
        <h1>{{ title }} </h1>
       
        <!-- <Button @btn-click="$emit('toggle-add-task')" 
        :text="showAddTask ?'Edit': 'Add Task'" 
        :color="showAddTask ? 'yellow':'green'"/> -->
      
    </header>
</template>


<script>
// import Add from './AddTask.vue'

export default {
    name: 'Header',
    props:{
        title: String,
        showAddTask: Boolean
    },
}
</script>


<style scoped>
    header {
        justify-content: space-between;
        align-content: center;
        margin-bottom: 20px;
    } 
   
</style>