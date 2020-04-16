<template>
  <li style="padding-right: 40px; padding-bottom: 20px;">
    <b-card style="box-shadow:10px 10px 5px grey;">
      <b-row>
        <b-col cols="10" align="left">
          <b-form-checkbox
            v-bind:checked="completed"
            v-on:change="$emit('change', $event)">
            <del v-if="completed"><slot></slot></del>
            <slot v-else></slot>
          </b-form-checkbox>
        </b-col>
        <b-col cols="2" align="right">
          <b-button size="sm" v-on:click="sendRemoveMessage()">
            <b-icon icon="x" style="width: 20px; height: 20px;"></b-icon>
          </b-button>
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
    prop: "completed",
    event: "change",
  },
  props: {
    completed: Boolean,
    title: String,
    id: Number
  },
  methods: {
    sendRemoveMessage() {
      this.$root.$emit('removeItem', this.id);
    }
  }
}
</script>