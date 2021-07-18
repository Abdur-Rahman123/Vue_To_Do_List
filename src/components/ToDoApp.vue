<template>
  <div class="container">
   <h2 class="text-center mt-5">My vue ToDoList</h2>
   <div class="d-flex">
    <input v-model="task" type="text" placeholder="Enter your Todo" class="form-control">
    <button @click="submitTask" class="btn btn-warning rounded-0">Submit</button>
  </div>
   <!--table-->
    <table class="table table-bordered mt-5">
  <thead>
    <tr>
      <th scope="col" class="text-center">Task</th>
      <th scope="col" class="text-center">Status</th>
      <th scope="col" class="text-center">#</th>
      <th scope="col" class="text-center">#</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="(task,index) in tasks" :key="index">
      <td class="text-center">
        <span :class="{ 'line-through': task.status === 'finished' }">{{task.name}}

        </span>
        </td>
       <td class="text-center">
         <span style="width: 120px" class="pointer" @click="chageStatus(index)" :class="{
                'text-danger': task.status === 'to-do',
                'text-success': task.status === 'finished',
                'text-warning': task.status === 'in-progress',
         }">
         {{task.status}}
           
         </span>
         </td>
        <td>
          <div class="text-center" @click="editTask(index)">
            <span class="fa fa-pen">

            </span>
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
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data(){
    return{
      task:'',
      editedTask:null,
      availabelStatuses:['to-do','in-progress','finished'],
      tasks: [
        {
          'name':'Steal banana from store',
          'status':'to-do'
        },
        {
          'name':'Steal orange from store',
          'status':'completed'
        }
      ]
    }
  },
  methods:{
    submitTask(){
     if(this.task.length==0)return;
     if(this.editedTask==null){
       this.tasks.push({
          name: this.task,
          status: "to-do",
        });
     }
     else{
         this.tasks[this.editedTask].name = this.task;
             this.editedTask = null;
     }
     this.task=null;
    },
    deleteTask(index){
      this.tasks.splice(index, 1);
    },
    editTask(index){
      this.task=this.tasks[index].name;
      this.editedTask=index;
      
    },
    chageStatus(index){
    let newindex=this.availabelStatuses.indexOf(this.tasks[index].status)
    if(++newindex>2){
      newindex=0;
    }
    this.tasks[index].status=this.availabelStatuses[newindex];
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.pointer{
  cursor: pointer;
}
.line-through{
  text-decoration: line-through;
}
</style>