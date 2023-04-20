import { createApp } from 'vue'
import App from './App.vue'
import './style.css'

createApp(App).mount('#app')






<script setup>
import { ref, computed } from 'vue'

let id = 0

const newTodo = ref('')
const hideCompleted = ref(false)
const todos = ref([
  { id: id++, text: 'Build Component', done: true },
  { id: id++, text: 'Create Project', done: false},
  
])

const filterTodo = computed(() => {
  return hideCompleted.value
    ? todos.value.filter((t) => !t.done)
    : todos.value
})

function addTodo() {
  todos.value.push({ id: id++, text: newTodo.value, done: false })
  newTodo.value = ''
}

function removeTodo(todo) {
  todos.value = todos.value.filter((t) => t !== todo)
}
</script>

<template>
  <main class="app">
    <section class="greeting">
			<h1 class="title"><b>
		TO DO LIST <br>ANANDA</b>
			</h1>
		</section>

    <section class="todo-list">
      
			<h3><b>TO DO LIST :</b></h3>
      <div v-for="todo in filterTodo" :class="`todo-item ${todo.done && 'done'}`">
					<label>
            <ul>
						<input type="checkbox" class="styled-checkbox" v-model="todo.done" >
						<span :class="{ done: todo.done }">{{ todo.text }}</span>
            </ul>
					</label>

					<div class="todo-content">
						<input type="text" v-model="todo.content" />
					</div>
					
					<div class="actions">
						<button class="delete" @click="removeTodo(todo)">Delete</button>
					</div>
				</div>
				<div>
				<button class="hide" @click="hideCompleted = !hideCompleted">
   				 {{ hideCompleted ? 'Show All' : 'Hide Completed' }}
  	</button></div>

		</section>
		
		
    <section class="create-todo">
			<h3><b>Fill In The Column Below!</b></h3>
  <form id="new-todo-form" @submit.prevent="addTodo">
    <input type="text" 
					name="content" 
					id="content" 
					placeholder="ex : Install Vue CLI" v-model="newTodo">
    <button class="tambah">Add To Do</button>
  </form>
  </section>

		
	</main>
	
</template>
<style>
.done {
  text-decoration: line-through;
}
</style>