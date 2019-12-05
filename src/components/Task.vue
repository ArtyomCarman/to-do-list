<template>
    <div class="d-flex">
        <v-text-field outlined 
                      v-model.trim="newTask"
                      label="Add new task" 
                      class="mr-2"
                      @keyup.enter="addNewTask"
                      ></v-text-field>
        <v-btn color="success" 
            height="56"
            outlined 
            class="px-12"
            @click='addNewTask'
            >Add</v-btn>
    </div>
</template>



<script>

export default {
  props:[
      'tasks'
  ],  
  data: () => ({
    newTask: ""
  }),
  
  methods: {
    addNewTask(){
        if (this.newTask.length != 0) {
            this.axios.post('http://localhost:3000/todo',{
                id:"",
                name: this.newTask,
                editStatus:false,
                done: false
            })
            .then((response) => {
                    this.tasks.push(response.data)
                  })
            this.newTask="";  
        }
    }
  }
};
</script>