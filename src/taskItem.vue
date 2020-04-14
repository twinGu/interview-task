<template>
  <li style="padding-right: 40px; padding-bottom: 20px;">
    <b-card style="box-shadow:10px 10px 5px grey;">
      <b-row>
        <b-col cols="3">
          <input 
            type="checkbox" 
            v-bind:checked="completed"
            v-on:change="$emit('change', $event.target.checked)">
        </b-col>
        <b-col cols="6">
          <p>{{ title }}</p>
        </b-col>
        <b-col cols="3">
          <b-button size="sm" v-on:click="$emit('remove')"><b-icon icon="x"></b-icon></b-button>
        </b-col>
      </b-row>
    </b-card>
  </li>
</template>

<script>

export default {
  name: 'taskItem',
  data () {
    return {
    };
  },
  model: {
    prop: 'completed',
    event: 'change'
  },
  props: {
    title: String,
    completed: Boolean,
    },
}


</script>