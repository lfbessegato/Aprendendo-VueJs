<template>
  <ul class="todo-list">
      <li v-for="(todo, index) in sortedTasks"
       class="todo" :key="index">
       <div class="view">
          <input class="toggle" @click="completeTask(todo)" type="checkbox">
          <label  v-if="todo.completed" class="todo-completed">{{ todo.title }}</label>
		  <label v-else >{{ todo.title }}</label>
       </div>
      </li>
  </ul>
</template>

<script>
import InputTask from './InputTask'
import { Task } from '../models/Task'

export default {
	props: ['todoList'],
	computed: {
		sortedTasks: function () {
			let sorted = this.todoList
			return sorted.sort(function (a, b){
				if (a.title < b.title) return -1
				if (a.title > b.title) return 1
				return 0
			})
		}
	},
	methods: {
		completeTask (task) {
			task.completed = !task.completed
		}
	}
}
</script>

<style>
.todo-completed {
	text-decoration: line-through;
}

</style>