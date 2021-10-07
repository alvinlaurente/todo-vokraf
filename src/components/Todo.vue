<template>
  <div class="container">
    <h2>Todo App</h2>
    <input v-model="task" type="text">
    <button v-on:click.prevent="submitTask(task)" class="btn btn-success">Submit</button>

    <input v-model="search" type="text">

    <input v-model="checked" type="checkbox">Checked
    <input v-model="unchecked" type="checkbox">Unchecked

    <table class="table">
      <thead>
        <tr>
          <th scope="col">Check</th>
          <th scope="col">Name</th>
          <th scope="col">Status</th>
          <th scope="col">Delete</th>
        </tr>
      </thead>
      <tbody>
        <tr :class="task.status ? 'done' : ''" v-for="(task, index) in filteredTasks" :key="index">
          <td><input v-model="task.status" type="checkbox"></td>
          <td>{{task.name}}</td>
          <td>{{task.status ? "done" : "ongoing"}}</td>
          <td><button class="btn btn-danger" v-on:click.prevent="deleteTask(index)">X</button></td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  data(){
    return{
      checked: false,
      unchecked: false,
      search: '',
      task: '',
      tasks: [
        {
          name: "Belajar",
          status: true,
        },
        {
          name: "Mandi",
          status: false,
        },
        {
          name: "Belajar 2",
          status: true,
        },
        {
          name: "Mandi 2",
          status: true,
        },
        {
          name: "Mandi 3",
          status: false,
        },
        {
          name: "Beli beras",
          status: false,
        }
      ],
    }
  },

  methods: {
    submitTask(task){
      this.tasks.push({
        name: task,
        status: false,
      })

      this.task = ''
    },
    deleteTask(index){
      this.tasks.splice(index, 1)
    },
  },

  computed: {
    filteredTasks(){
      if (this.checked || this.unchecked || this.search){
      return this.tasks.filter((task) => {
        return task.status === this.checked && task.status !== this.unchecked && task.name.toLowerCase().includes(this.search.toLowerCase());
      })
      }
      return this.tasks ;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.done {
  background-color: red;
}
</style>
