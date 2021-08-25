<template>
    <form @submit="onSubmit" class="add-form">
        
        <div class="input-group mb-3">
            <input type="text" v-model="text" class="form-control" placeholder="Add Task" aria-label="Add Task" aria-describedby="button-addon2">
            <button type="submit" value="Save Task" class="btn btn-success" id="button-addon2"><i class="fa fa-plus"></i></button>
            
        </div>
        <input type="datetime-local"  v-model="value" name="date">
    </form> 

    
</template>

<script>
export default {
    name: 'AddTask',
    data(){
        return{
            text:'',
            value:''
        }
    },
    methods: {
        onSubmit(e){
            e.preventDefault()
            if(!this.text){
                alert('plase add a task');
                return false;
            }
            const newTask = {
                id: Math.floor(Math.random()*100000),
                text: this.text,
                value: this.value,

            }
            this.$emit('add-task',newTask)
            this.text = '',
            this.value = ''
        }

    },
    
}
</script>