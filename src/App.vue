<template>
	<div id="app">
		<Header />
		<div class="container">
			<Input
				v-on:addItem="addTodo"
				v-on:markAllDone="markAllDone"
			/>
			<Todos
				v-bind:todos="filteredTodos"
				v-on:removeTodo="removeTodo"
				v-on:markDone="markDone"
				@saveTodos="saveTodos"
			/>
			<BottomNav
				v-on:filterAll="filterAll"
				v-on:filterActive="filterActive"
				v-on:filterCompleted="filterCompleted"
				v-on:clearCompleted="clearCompleted"
				v-bind:filteredTodos="filteredTodos"
			/>
		</div>
		<Footer />
	</div>
</template>

<script>
	import Header from './components/Header'
	import Input from './components/Input'
	import Todos from './components/Todos'
	import BottomNav from './components/BottomNav'
	import Footer from './components/Footer'

	let key = 'brandbotassessmentkey'
	let data = JSON.parse(localStorage.getItem(key)) || []


	export default {
		name: 'App',
		components: {
			Header,
			Input,
			Todos,
			BottomNav,
			Footer
		},
		data: function() {
			return {
				todos: data,
				filteredTodos: data,
				// activeTodos: this.filterActive(),
				// completedTodos: this.filterCompleted()
			}
		},
		methods: {
			saveTodos() {
				this.filteredTodos = this.todos
				localStorage.setItem(key, JSON.stringify(this.todos))
			},
			addTodo(item) {
				let newItem = this.createTodoObject(item)
				this.todos = [...this.todos, newItem]
				this.saveTodos()
			},
			createTodoObject(todo) {
				let todoObject = {
					id: Math.floor(Math.random() * 100000000),
					name: todo,
					done: false
				}
				return todoObject
			},
			removeTodo(id) {
				this.todos = this.todos.filter(todo => todo.id != id)
				this.saveTodos()
			},
			markDone(id) {
				let item
				for (let obj of this.todos) {
					if (obj.id === id) {
						item = obj
					}
				}
				item.done = !item.done
				this.saveTodos()
			},
			markAllDone() {
				let doneArray = []
				for (let obj of this.todos) {
					if (obj.done === false) {
						doneArray.push(obj.done)
					}
				}
				
				if (doneArray.includes(false)) {
					for (let obj of this.todos) {
						obj.done = true
					}
				} else {
					for (let obj of this.todos) {
						obj.done = false
					}
				}
				this.saveTodos()
			},
			filterAll() {
				this.filteredTodos = this.todos
			},
			filterActive() {
				this.filteredTodos = this.todos.filter(todo => todo.done !== true)
			},
			filterCompleted() {
				this.filteredTodos = this.todos.filter(todo => todo.done !== false)
			},
			clearCompleted() {
				for (let obj of this.todos) {
					if (obj.done === true) {
						this.removeTodo(obj.id)
					}
				}
			}
		}
	}
</script>

<style>
	body {
		margin: 0;
		padding: 0;
		background-color: #f3f3f3;
		width: 100%;
		height: 100%;
		text-align: center;
	}
	.container {
		height: 80%;
		width: 80%;
		margin: auto;
	}
</style>
