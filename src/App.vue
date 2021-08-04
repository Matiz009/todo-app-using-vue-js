<template>
          <div class="jumbotron bg-primary text-light">
           <div class="container">
            <b>
              <h1 class="display-4">Todo App</h1>
              <p class="lead">Manage daily tasks with ease</p>
            </b>
           </div>
          </div>
          <div class="container">
            <div class="row">
              <div class="col-md-4">
                <input type="text" name="" id="taskip" @keydown.enter="insertItem" v-model="todoItem" placeholder="Add task here!">
              </div>
            </div> <br><br>
    
            <div class="row">
              <div class="col-md-12">
                <h3>Tasks List</h3>
                <table class="table table-striped">
                  <thead class="thead-dark">
                   <th>ID</th>
                   <th>Name</th>
                    <th>Mark as Done</th>
                    <th>Delete</th>
                   

                  </thead>
                  <tbody>
                    <tr v-for="(task,index) in todoList" v-bind:key="task">
                      <td>{{task.id}}</td>
                      <td><div v-if="!task.editing" v-on:dblclick="editTask(task)" v-bind:class="{completed: task.isCompleted}">{{task.name}}</div>
                      <input v-model="task.name" v-else type="text">
                      </td>
                      <td><input @blur="editCompleted(task)" @keydown.enter="editCompleted(task)" v-model="task.isCompleted" type="checkbox"></td>
                      <td><button @click="removeItem(index)" class="btn btn-sm btn-danger">Delete</button></td>
                    </tr>
                  </tbody>
                </table>
              </div>
            </div>
          </div>
</template>

<script>


export default {
  data(){
    return {
      todoItem: '',
      id:0,
      todoList: [],

    }
  },
  methods: {
    insertItem(){
     console.log(this.todoItem);
     this.todoList.push({name:this.todoItem,isCompleted:false,id:this.id,editing:false});
     this.id++;
     this.todoItem = '';
    },
    editTask(task){
      task.editing = true;
    },
    editCompleted(task){
      task.editing = false;
    },
    removeItem(index){
      this.todoList.splice(index,1);
    }
  }
}
</script>

<style>
.completed{
  text-decoration: line-through;
  color: grey;

}
#taskip{
  border: none;
  border-bottom: 1px solid #ccc;
  border-color: black;

}
</style>
