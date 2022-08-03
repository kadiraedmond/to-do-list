<template>
  <div class="container">
   <H2 class="text-center mt-5"> My Vue todo App</H2>  
   <!-- imput -->
    <div class="d-flex">
       <input  v-model="task" type="text" placeholder="enter task" class="form-control">
       <button @click="submitTask" class="btn btn-warning rounded-0"> SUBMIT</button> 
    </div> 
    <!-- task -->
    <table class="table table-bordered mt-5">
  <thead>
    <tr>
      <th scope="col">Task</th>
      <th scope="col">status</th>
      <th scope="col" class="text-center">#</th>
      <th scope="col" class="text-center">#</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="(task, index) in tasks" :key="index">
      <td>{{task.name}}</td>
      <td>
        <span @click= "changestatus(index)" class="pointer">
          {{task.status}}
        </span>
      </td>
      <td>
        <div class="text-center" @click="editTask(index)">
          <span class="fa fa-pen"></span> 
        </div> 
      </td>
      <td>
         <div class="text-center" @click="deleteTask(index)">
          <span class="fa fa-trash"></span> 
        </div> 
      </td>
    </tr>
     
  </tbody>
</table>
  </div>   
</template>

<script>
export default {
  name: ' TodoApp',
  props: {
    msg: String
  },

  data(){
    return {
      task: 'Hello world',
      editedTask: null,
      availalablestatuse: ['to-do', 'in-progress', 'finished'],

      tasks:[
        {
          name: 'style bananas from the store.',
          status: 'to-do'

        },
        {
          name: 'Eat 1kg chocola.',
          status: 'in progress',

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
              status: 'to-do'
          });

          }else{
            this.tssks[this.editedTask].name = this.task;
            this.editedtask = null;
          }

          this.task ='';
       },
       deleteTask(index){
          this.tasks.splice(index, 1);
       },

        editTask(index){
          this.task = this.tasks[index].name;
          this.editedTask = index;

       },

       changestatus(index){
        let newIndex = this.availalablestatuse.indexOf(this.tasks[index].status);
        if(++newIndex > 2 ) newIndex =0;
        this.tasks[index].status =this.availablestatuses[newIndex];

       },
       
    },
  
}
</script>

 
<style scoped>
.pointer {
  cursor:pointer;
}
 
</style>
