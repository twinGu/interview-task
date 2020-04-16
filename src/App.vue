<template>
  <div id="app">
    <h1>TO-DO List</h1>
    <form v-on:submit.prevent="addNewTask">
      <b-input 
      v-model="newTask" 
      :state=textLength 
      id=new-task 
      placeholder="Write your task here" 
      style="margin: 0 auto; width: 200px; box-shadow:5px 5px 5px grey;">
      </b-input><br>
      <b-button :disabled=!textLength type="submit" variant="primary">Add task</b-button>
    </form>
    <task-holder :tasks=openTasks>Not finished tasks</task-holder>
    <task-holder :tasks=completedTasks>Finished tasks</task-holder>
  </div>
</template>

<script>
import taskHolder from './taskHolder.vue'

export default {
  name: 'app',
  mounted () {
    this.$root.$on('removeItem', (id) => {
      this.tasks = this.tasks.filter(function(obj){ return obj.id != id;})
    });
  },
  components: {
    taskHolder
  },
  data () {
    return {
      newTask: '',
      tasks: [],
      nextTaskId: 1,
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
    },
    textLength() {
        return this.newTask.length > 0 ? true : false
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
