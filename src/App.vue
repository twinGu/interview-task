<template>
  <div id="app" align="center">
    <h1>TO-DO List</h1>
    <form v-on:submit.prevent="addNewTask">
      <b-input v-model="newTask" id=new-task placeholder="Write your task here" style="box-shadow:5px 5px 5px grey;"></b-input><br>
      <b-button type="submit" variant="primary">Add task</b-button>
    </form>
    <h2>Not finished tasks</h2>
    <ul style="list-style-type:none;">
      <li is="taskItem"
      v-for="task in openTasks"
      v-bind:key="task.id"
      v-bind:title="task.title"
      v-on:remove="tasks = tasks.filter(function(obj){ return obj.id != task.id;})"
      v-model="task.isCompleted"
      ></li>
    </ul>
    <h2>Finished tasks</h2>
    <ul style="list-style-type:none;">
      <li is="taskItem"
      v-for="task in completedTasks"
      v-bind:key="task.id"
      v-bind:title="task.title"
      v-on:remove="tasks = tasks.filter(function(obj){ return obj.id != task.id;})"
      v-model="task.isCompleted"
      ></li>
    </ul>
  </div>
</template>

<script>
import taskItem from './taskItem.vue'

export default {
  name: 'app',
  components: {
    taskItem
  },
  data () {
    return {
      newTask: '',
      tasks: [
        {
          id: 1,
          title: 'Do the dishes',
          isCompleted: false,
        },
        {
          id: 2,
          title: 'Take out the trash',
          isCompleted: false,
        },
        {
          id: 3,
          title: 'Mow the lawn',
          isCompleted: false,
        }
      ],
      nextTaskId: 4,
    };
  },
  computed: {
    openTasks: function () {
      return this.tasks.filter(function (task) {
        return !task.isCompleted
      })
    },
    completedTasks: function () {
      return this.tasks.filter(function (task) {
        return task.isCompleted
      })
    }
  },
  methods: {
    addNewTask: function () {
      this.tasks.push({
        id: this.nextTaskId++,
        title: this.newTask
      })
      this.newTask = ''
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #797979;
  margin-top: 60px;
}
</style>
