<script setup>
import { ref, onMounted } from 'vue';

const name = ref("suraj");
const status = ref("active");
const tasks = ref(["task1", "task2", "task3"]);
const bind = ref("https://www.google.com");
const newTask = ref('');

const toggleStatus = () => {
  status.value = status.value === 'active' ? 'inactive' : 'active';
}

const addTask = () => {
  if (newTask.value.trim() !== '') {
    tasks.value.push(newTask.value);
    newTask.value = '';
  }
}

const deleteTask = (index) => {
  tasks.value.splice(index, 1);
}

onMounted(async () => {
  try {
    const response = await fetch('https://jsonplaceholder.typicode.com/todos');
    const data = await response.json();
    tasks.value = data.map((task) => task.title);

  } catch (error) {
    console.error('Error fetching tasks:', error);
  }
});

</script>

<template>
  <h2>{{ name }}</h2>
  <h3 v-if="status === 'active'">Active</h3>
  <h3 v-else-if="status === 'pending'">User is pending</h3>
  <h3 v-else>User is inactive</h3>

  <form @submit.prevent="addTask">
    <label for="newTask">Add Task</label>
    <input type="text" id="newTask" name="newTask" v-model="newTask" />
    <button type="submit">Submit</button>


  </form>

  <h3>Tasks:</h3>
  <ul>
    <li v-for="(task, index) in tasks" :key="task">
      <span>
        {{ task }}
      </span>
      <button @click="deleteTask(index)">Delete</button>
    </li>
  </ul>
  <!-- <a v-bind:href="bind">Google</a> -->
  <a :href="bind">Google</a>
  <!-- <button v-on:click="toggleStatus">Clicked me to toggle</button> -->
  <button @click="toggleStatus">Clicked me to toggle</button>
</template>
