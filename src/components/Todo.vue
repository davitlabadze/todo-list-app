<template>
    <div class="container">
        <h2 class="text-center mt-5">Todo App</h2>

         <!-- input -->
        <div class="d-flex">
            <input v-model="task" type="text" placeholder="Enter Task" class="form-control">
            <button @click="submitTask" 
            :class="{'btn btn-success': this.update==false, 
                     'btn btn-warning': this.update==true}">
            <i :class="{ 'fa fa-plus': this.update==false,
                         'fa fa-pen': this.update==true }"></i>
            
            </button>
        </div>

        <!-- task table -->

        <table class="table mt-5">
            <!-- <thead>
                <tr>
                <th scope="col">task</th>
                <th scope="col">status</th>
                <th scope="col" class="text-center">#</th>
                <th scope="col" class="text-center">#</th>
                </tr>
            </thead> -->
            <tbody > 
                <tr v-for="(task,index) in this.tasks" :key="index">
                    <th>
                        <span :class="{'finished': task.status === 'finished'}">
                            {{ task.name }}
                        </span>
                    </th>
                    <td style="width: 120px">
                        <span @click="changeStatus(index)" class="pointer"
                        :class="{'text-danger': task.status === 'to-do',
                        'text-warning': task.status === 'in-progress',
                        'text-success': task.status === 'finished',
                        
                        }">
                            {{ firstCharUpper(task.status) }}
                        </span>
                    </td>
                    <td>
                        <div @click="editTask(index)" class="text-center">
                            <i class="fa fa-pen pointer" style="color:orange"></i>
                        </div>
                    </td>
                    <td>
                        <div @click="deleteTask(index)" class="text-center">
                            <i class="fa fa-trash pointer" style="color:red"></i>
                        </div>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
 
    
</template>

<script>
export default {
    name: "Todo",

      data() {
      return {
          task: '',
          theme: '',
          editedTask: null,
          update: false,
          availableStatuses: ['to-do', 'in-progress', 'finished'], 
          tasks: [
              {
                  name: 'test1',
                  status: 'to-do'
              },
              {
                  name: 'test2',
                  status: 'in-progress'
              },
              {
                  name: 'test3',
                  status: 'finished'
              }
          ]
      }
    },
    
 

    methods: {
        submitTask(){
            
            if(this.task.length === 0) return;

            if(this.editedTask === null){
                this.tasks.push({
                    name: this.task,
                    status: "to-do"
                });
            }else{
                this.tasks[this.editedTask].name = this.task;
                this.editedTask = null;
            }
            this.task = '';
            this.update = false;
        },

        changeStatus(index){
           let newIndex = this.availableStatuses.indexOf(this.tasks[index].status);
           if(++newIndex>2) newIndex = 0;
           this.tasks[index].status = this.availableStatuses[newIndex];
        },

        firstCharUpper(str){
            return str.charAt(0).toUpperCase() + str.slice(1);
        },

        editTask(index){
            this.task = this.tasks[index].name;
            this.editedTask = index;
            this.update = true;
        },


        deleteTask(index){
            if(confirm('Are you sure?')){
            this.tasks.splice(index,1);
            }   
        },
    },
    
   
}
</script>

<style>

.pointer{
    cursor: pointer;
}

.finished {
    text-decoration: line-through;
    opacity: .5;
}
</style>