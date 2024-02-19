<template>
  <div class="container">
    <h2 class="text-center mt-5">My Vue Todo App</h2>
    
    <div class="d-flex">
      <input v-model="task" type="text" placeholder="Enter text" class="form-control">
      <button @click="submitTask" class="btn btn-warning rounded-0">SUBMIT</button>
    </div>


    <!-- table -->
    <table class="table table-bordered mt-5">
      <thead>
        <tr>
          <th scope="col">Task</th>
          <th scope="col">Status</th>
          <th scope="col" class="text-center">Update</th>
          <th scope="col" class="text-center">Delete</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(task,index) in tasks" :key="index">
          <th>{{task.name}}</th>
          <td style="width:120px">
            <span class="pointer" @click="updateStatus(index)">
              {{firstCharUpper(task.status)}}
            </span>
          </td>
          <td>
            <div @click="editTask(index)" class="text-center">
              <span class="fa fa-pen"></span>
            </div>
          </td>
          <td>
            <div @click="deleteTask(index)" class="text-center">
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
      availabeStatuses:['to-do','in-progress','finished'],
      task:'',
      editedTasks:'',
      tasks: [
        {
          name:'steal bananas',
          status: 'to-do'
        },
        {
          name:'create an iron man suit',
          status: 'in-progress'
        }
      ]
    }  
  },
  methods:{
    submitTask(){
      if(this.task.length === 0) return;

      if(this.editedTask===null){
        this.tasks.push({
          name: this.task,
          status:"to-do"
        })
      }else{
        this.tasks[this.editedTask].name=this.task
        this.editedTask=null

      }

      // delete all the input field once you have submitted 
      this.task = ''

    },
    deleteTask(index){
      // if(this.tasks.length === 0)return;

      this.tasks.splice(index,1)
    },
    editTask(index){
      this.editedTask = index
      this.task=this.tasks[index].name

    },
    updateStatus(index){
      let newIndex = this.availabeStatuses.indexOf(this.tasks[index].status)
      if(++newIndex>2) newIndex =0
      this.tasks[index].status = this.availabeStatuses[newIndex]

    },
    firstCharUpper(){
      
    }
    
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.pointer{
  cursor: pointer;
}
</style>
