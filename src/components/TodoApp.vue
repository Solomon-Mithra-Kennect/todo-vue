<template>
  <div calss="container">
    <h2 class="text-center mt-5">My Vue TodoApp</h2>
    
    <!-- input -->
    <div class="d-flex justify-content-center">
      <div class="d-flex col-11 col-lg-6 col-md-9 col-sm-11 mt-2">
        <input v-model="task" type="text" placeholder="Enter Text" class="form-control">
        <button @click="submitTask" class="btn btn-warning rounded-0">SUBMIT</button>
      </div>
    </div>

    <!-- table -->
    <div class="d-flex justify-content-center mt-5">
      <div class="col-11 col-lg-9">
          <table class="table table-bordered col-7">
        <thead>
          <tr>
            <th scope="col">Task</th>
            <th scope="col">Status</th>
            <th scope="col" class="text-center">#</th>
            <th scope="col" class="text-center">#</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(task, index) in tasks" :key="index">
            <td>{{ task.name }}</td>
            <td style="width: 120px">
              <span class="pointer" @click="changeTask(index)">{{ task.status }}</span>
            </td>
            <td class="text-center" @click="editTask(index)"><span class="fa fa-pen"></span></td>
            <td class="text-center" @click="deleteTask(index)"><span class="fa fa-trash"></span></td>
          </tr>
          
        </tbody>
      </table>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'TodoApp',
  props: {
  },
  data(){
    return{
      task:'',
      editedTask: '',
      availableStatus: ['to-do', 'In-progress', 'Completed'],
      tasks: [
        {
          name: 'Buy chocolates from the store',
          status: 'to-do'
        },
        {
          name: 'Eat chocolate',
          status: 'to-do'
        }
      ]
    }
  },
  methods:{
    submitTask(){
      if(this.task.length === 0)
        return;
      
      if(this.editedTask === ''){
        this.tasks.push({
          name: this.task,
          status: 'to-do'
        })
      }else{
        this.tasks[this.editedTask].name = this.task;
        this.editedTask = '';
      }
        this.task = '';
    },
    deleteTask(index){
        this.tasks.splice(index,1);
    },
    editTask(index){
      this.task = this.tasks[index].name;
      this.editedTask = index;
    },
    changeTask(index){
      let newIndex = this.availableStatus.indexOf(this.tasks[index].status);
      if(++newIndex > 2) newIndex = 0;
      this.tasks[index].status = this.availableStatus[newIndex];
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
