<template>
  <v-list>
    <v-list-item v-for="task in tasks" :key="task.id">
      <v-list-item-action>
        <v-checkbox color="pink" v-model="task.done"></v-checkbox>
      </v-list-item-action>
      <v-list-item-content
        :style="[task.done ? doneStyle:'']" 
        @click='editTask(task)'
        v-if="!task.editStatus"
      >{{task.name}}
      </v-list-item-content>
        <v-text-field
        @keyup.esc="updateTask(task)"
        @keyup.enter='updateTask(task)'
        v-else
        autofocus
        v-model="task.name"
        dense
      ></v-text-field>
      <v-list-item-action>
        <v-icon color="success" v-show="task.done">mdi-check</v-icon></v-list-item-action>
      <v-list-item-action>
        <v-btn  color="error"
                @click='deleteTask(task)'>
          <v-icon>mdi-close</v-icon>
        </v-btn></v-list-item-action>
    </v-list-item>
  </v-list>
</template>

<script>
export default {
  props:[
     'tasks' 
  ],  
  data: () => ({
      doneStyle: {
        color: 'lightgray',
        textDecoration: 'line-through'
      },
  }),
  methods: {
    deleteTask(task) {
      var index = this.tasks.indexOf(task);
      this.tasks.splice(index, 1);
      this.axios.delete("http://localhost:3000/todo/" + task.id);
    },
    editTask(task) {
      task.editStatus=true
    },
    updateTask(task){
      this.axios.put('http://localhost:3000/todo/'+task.id, task)
      task.editStatus = false
    }
  },
};
</script>