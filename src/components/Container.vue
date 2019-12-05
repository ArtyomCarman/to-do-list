<template>
  <v-container>
    <v-card max-width="500" class="mx-auto pa-2" > 
      <Task :tasks='tasks'></Task>
      <List :tasks='tasks'></List>
    </v-card>
  </v-container>
</template>

<script>
import Task from './Task';
import List from './List';

export default {
  name: 'Container',

  components: {
    Task,
    List
  },

  data: () => ({
    tasks: []
  }),
  mounted: function () {
  this.$nextTick(function () {
    var vm = this;
    this.axios.get("http://localhost:3000/todo")
              .then(function(response) {
                vm.tasks = response.data;
              })
  })
}
};
</script>
