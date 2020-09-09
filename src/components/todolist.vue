<template>
  <div>
    <h1>{{ msg }}</h1>

    <CreateTask :items="items"/> <!-- Передать параметр items в модуль CreateTask-->
    <TaskList 
      :items="items"
      @deleteTask="deleteTask"
    />


  </div>
</template>

<script>
const axios = require('axios').default;
import CreateTask from '@/components/CreateTask'
import TaskList from '@/components/TaskList'

export default {
  name: "todolist",

  components: {
    CreateTask,
    TaskList
  },

  mounted() {
    axios
      .get('https://jsonplaceholder.typicode.com/users/1/todos')
      .then(response => (this.items = response.data));

      //this.$emit('items', items) // Данные которые будут возвращаться в родительский модуль
    
  },

  data() {
    return {
      msg: "TodoList Launch",
      items: []
    };
  },

  methods: {
    deleteTask(index) {
      this.items.splice(index, 1);
    }
  }

};
</script>

<style>
</style>