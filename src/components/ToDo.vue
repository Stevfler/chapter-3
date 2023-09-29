<script setup>
import {ref, computed } from 'vue';

const
	_todo_text = ref(""),
	_todo_list = ref([]),
	_pending = computed(() => {
		return _todo_list.value.filter(item => !item.checked)
	}),
	_done = computed(() => {
		return _todo_list.value.filter(item => item.checked)
	})

function clearToDo(params) {
	_todo_text.value = ""
}
function addToDo(params) {
	if (_todo_text.value && _todo_text.value !== '') {
		_todo_list.value.push({
			id: new Date().valueOf(),
			text: _todo_text.value,
			checked: false
		})
		clearToDo()
	}
}
</script>
<template>
	<div class="todo-container w3-white w3-card-4">
		<!--Simple header -->
		<div class="w3-container w3-black w3-margin-0 w3-bottombar w3-border-blue">
			<h1>
				<i class="fa-solid fa-clipboard-list"></i> To-Do List
			</h1>
		</div>
		<!-- User input	-->
		<div class="w3-container flex-container w3-light-gray w3-padding">
			<input type="text" class="w3-input w3-border-0" placeholder="Type here your to-do item..."
			autofocus
			v-model="_todo_text"
			@keydown.enter="addToDo()"
			>
			<button class="w3-button w3-gray" @click="clearToDo()">
				<i class="fa-solid fa-times"></i>
			</button>
			<button class="w3-button w3-blue" @click="addToDo()">
				<i class="fd-solid fa-plus"></i>
			</button>
		</div>

		<!-- list of pending items -->
		<div class="w3-padding w3-blue">Pending ({{ _pending.length }})</div>
		<div class="w3-padding" v-for="todo in _pending" :key="todo.id">
			<label>
				<input type="checkbox" v-model="todo.checked">
				<span class="w3-margin-left"> {{ todo.text }} </span>
			</label>
		</div>
		<div class="w3-padding" v-show="_pending.length == 0"> No tasks </div>

		<!-- list done task -->
		<div class="w3-padding w3-blue"> Done task(s) ({{ _done.length }})</div>
		<div class="w3-padding" v-for="todo in _done" :key="todo.id">
				<label>
					<input type="checkbox" v-model="todo.checked">
					<span class="w3-margin-left"> {{ todo.text }} </span>
				</label>
			</div>
		<div class="w3-padding" v-show="_done.length == 0"> No tasks </div>
	</div>
</template>
<style scoped>
.todo-container{
	display: flex;
	width: 100%;
	max-width: 600px;
	flex-direction: column;
	
}
.flex-container{
	display: flex;
	flex-direction: row;
}
</style>