<template>
  <div class="container">
    <div v-if="messages !== ''" class="alert alert-danger" role="alert" >
      {{ messages }}
    </div>
    <div class="add-task">
      <input type="text" id="title" placeholder="Input title" required>
      &nbsp;&nbsp;&nbsp;
      <button class="btn btn-primary" v-on:click="addTask">Add new task</button>
      &nbsp;&nbsp;&nbsp;
      <button class="btn btn-warning" v-on:click="updateTask">Update task</button>
    </div>
    <br><br><br>
    <list-task 
    v-bind:tasks="tasks"
    v-on:getDataUpdate="getDataUpdate"
    v-on:getIdDelete="getIdDelete"/>
  </div>
</template>

<script>
import ListTask from "./components/ListTaskComponent.vue";
export default {
  name: 'App',
  components: {
    ListTask,
  },
  data() {
    return {
      messages : '',
      tasks : [
        {
          id : 0,
          title : "Hoc Lap Trinh"
        }, 
        {
          id : 1,
          title : "Di tam"
        },
        {
          id : 2,
          title : "Di ngu"
        }
      ],
      edit_id : 0
    }
  },
  methods : {
    addTask() {
      var title = document.getElementById("title").value;
      if (title === "" || title === "undefined") {
        this.messages = "Input Title please"
      } else {
        this.messages = "";
        var id = this.tasks.length;
        console.log(id);
        this.tasks.push({
          id : id,
          title : title
        });
        document.getElementById("title").value = "";
      }
      
    },
    getDataUpdate(data) {
        document.getElementById("title").value = data.title;
        this.edit_id = data.id;
    },
    updateTask() {
        var title = document.getElementById("title").value;
        if (title === "" || title === "undefined") {
          this.messages = "Input Title please"
        } else {
          this.messages = "";
          this.tasks.forEach(task => {
          if (task.id === this.edit_id) {
            task.title = title;
          }
          })
          document.getElementById("title").value = "";
        }
    },
    getIdDelete(data) {
      for (var i = 0; i < this.tasks.length; i++) {
        if (this.tasks[i].id === data) {
          this.tasks.splice(i,1);
        }
      }
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
