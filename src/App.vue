<script setup>
import { onMounted, ref } from 'vue'

const tasks = ref(['Task One', 'Task Two', 'Task Three'])
const newTask = ref('')
const handleTaskSub = () => {
  if (newTask.value !== '') {
    tasks.value.push(newTask.value)
    newTask.value = ''
  } else {
    alert("Oop's something is wrong, trying adding a task or increase your task length.")
    newTask.value = ''
  }
}
const deleteTasks = (id) => {
  tasks.value.splice(id, 1)
}

onMounted( async () => {
  try {
    const response = await fetch('https://jsonplaceholder.typicode.com/todos')
    const data = await response.json()
    tasks.value = data.map((item) => item.title)
    console.warn(data);
    // console.warn(t);
  } catch (error) {
    console.log(error);
  }
})
</script>

<template>
  <h2>VueTasksify</h2>
  <form @submit.prevent="handleTaskSub">
    <label for="Tasks">Task</label>
    <input type="text" v-model="newTask" placeholder="Add a tasks">
    <button type="submit" style="background: springgreen;">Add new tasks</button>

  </form>
  <ul>
    <li v-for="(item, index) in tasks" :key="index" >{{ item }} <button @click="deleteTasks(index)">delete</button></li>
  </ul>
</template>

<style scoped>
.content {
  text-align: center;
}
</style>
