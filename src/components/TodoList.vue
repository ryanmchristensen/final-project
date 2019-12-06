<template>
	<div>
		<BaseInputText 
			v-model="newTodoText"
			placeholder="New todo"
			@keydown.enter="addTodo"
		/>
		<ul v-if="todos.length">
			<TodoListItem
				v-for="todo in todos"
				:key="todo.id"
				:todo="todo"
				@remove="removeTodo"
			/>
		</ul>
		<p v-else>
			Add a todo!
		</p>
	</div>
</template>

<script>
import axios from 'axios';
import BaseInputText from './BaseInputText.vue'
import TodoListItem from './TodoListItem.vue'

let nextTodoId = 1

export default {
  name: 'HelloWorld',
	components: {
		BaseInputText, TodoListItem
	},
  data() {
    return {
			newTodoText: '',
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
		addTodo () {
			const trimmedText = this.newTodoText.trim()
			if (trimmedText) {
				this.todos.push({
					id: nextTodoId++,
					title: trimmedText
				})
				this.newTodoText = ''
			}
		},
		removeTodo (idToRemove) {
			this.todos = this.todos.filter(todo => {
				return todo.id !== idToRemove
			})
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
  text-align: left;
}
</style>
