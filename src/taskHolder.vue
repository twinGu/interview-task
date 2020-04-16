<template>
  <div v-if="tasks.length > 0" id=task-holder>
    <h2><slot></slot></h2>
    <ul style="list-style-type:none;">
      <li is="taskItem"
      v-for="task in tasks"
      v-bind:key="task.id"
      v-bind:id="task.id"
      v-bind:title="task.title"
      v-model="task.isCompleted"
      >{{task.title}}</li>
    </ul>
  </div>
</template>

<script>
import taskItem from './taskItem.vue'

export default {
  name: 'task-holder',
  components: {
    taskItem
  },
  data: function () {
    return {
    }
  },
  props: {
    tasks: Array
  },
}
</script>