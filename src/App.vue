<template>
	<div class="todo-wrapper w-50 mx-auto border border-white rounded p-3">
		<h1>Tasks List</h1>
		<form action="" @submit.prevent="handleAddTask" class="mb-4 d-flex justify-content-center column-gap-3">
			<input type="text" v-model="taskInput">
			<button type="submit" class="btn btn-primary">Add</button>
		</form>
		<div class="task-counter d-flex column-gap-3 justify-content-center">
			<span>All ({{ taskCounter.all }})</span>
			<span>Completed ({{ taskCounter.completed }})</span>
			<span>Remaining ({{ taskCounter.all - taskCounter.completed }})</span>
		</div>
		<Tasks :taskList="tasksArr" @edit="editTask" @delete="deleteTask"/>
		<div v-if="showModal">
			<Modal :taskToEdit="currentTaskToEdit" @saved="updateTask" @close="toggleModal"/>
		</div>
	</div>
</template>

<script>
import Modal from './components/Modal.vue'
import Tasks from './components/Tasks.vue'

export default {
	name: 'App',

	components: { Modal, Tasks},

	data() {
		return {
			taskInput: '',
			tasksArr: [],
			currentTaskToEdit: '',
			showModal: false,
		}
	},

	methods: {
		handleAddTask() {
			if (this.taskInput) {
				this.tasksArr.push({name: this.taskInput, isComplete: false})
				this.taskInput = ''
			}
		},

		deleteTask({ task }) {
			const indexToDelete = this.tasksArr.indexOf(task)
			this.tasksArr.splice(indexToDelete, 1)      
		},

		toggleModal() {
			this.showModal = !this.showModal
		},

		editTask({ task }) {
			this.currentTaskToEdit = task
			this.toggleModal()
		},

		updateTask({ val }) {
			this.currentTaskToEdit.name = val
		}
	},

	computed: {
		taskCounter() {
			return {
				all: this.tasksArr.length,
				completed: this.tasksArr.filter(task => {return task.isComplete}).length
			}
		}
	}

}
</script>

<style>
	body {
		background-color: #282a37;
	}

	#app {
		font-family: Avenir, Helvetica, Arial, sans-serif;
		-webkit-font-smoothing: antialiased;
		-moz-osx-font-smoothing: grayscale;
		text-align: center;
		color: #e2eaf2;
		margin-top: 60px;
	}
</style>
