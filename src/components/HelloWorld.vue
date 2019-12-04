<template>
  <div class="hello">
    <h3 style="text-align: center;"><u>Todo list:</u></h3>
    <ul v-for="todo in todos" v-bind:key="todo.id" class="list">
      <li>{{ todo.title }}</li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'HelloWorld',

  data() {
    return {
    todos: [],
    }
  },
  mounted() {
    axios.get('http://localhost:3000/todos').then((result) => {
      this.todos = result.data;
    }).catch((err) => {
      console.log(err);
    });    
  },
  methods: {
    addTodo(item) {
      return this.todos = this.todos.push(item);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
.hello{
  padding-left: 50em;
  text-align: left;
}
</style>
