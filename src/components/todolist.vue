<script setup lang="ts">
import { ref } from 'vue'

interface Task {
  id: number
  name: string
  done: boolean
}

const tasks = ref<Task[]>([])

const newTask = ref({
  name: '',
  done: false
})

const addTask = () => {
  if (newTask.value.name) {
    tasks.value.push({
      id: Date.now(), 
      name: newTask.value.name,
      done: newTask.value.done 
    })
    newTask.value.name = ''
    newTask.value.done = false
  }
}

const toggleTask = (task: Task) => {
  task.done = !task.done
}
</script>

<template> 
  <div>
    <div>TaskList</div>
    <ul>
      <li 
        v-for="task in tasks" 
        :key="task.id" 
        @click="toggleTask(task)"
        :class="{ 'done-task': task.done }"
      >
        <div>名前: {{ task.name }}</div>
        <div>完了: {{ task.done ? 'はい' : 'いいえ' }}</div>
      </li>
    </ul>
    <div>
      <label>
        名前:
        <input v-model="newTask.name" type="text" @keyup.enter="addTask" />
      </label>
      <label>
        完了:
        <input v-model="newTask.done" type="checkbox" />
      </label>
      <button @click="addTask">add</button>
      </div>
  </div>
</template>

<style>
li {
  cursor: pointer;
  padding: 8px;
  border-bottom: 1px solid #ccc;
}

li:hover {
  background-color: #f0f0f0;
}

.done-task {
  text-decoration: line-through;
  color: #888;
}
</style>