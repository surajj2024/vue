<script>
export default {
  data() {
    return {
      name: "suraj",
      status: 'pending',
      tasks: ["task1", "task2", "task3"],
      bind: "https://www.google.com",
    }
  },
  methods: {
    toggleStatus(){
      this.status = this.status === 'active' ? 'inactive' : 'active';
    }
  },
}

</script>

<template>
  <h2>{{ name }}</h2>
  <h3 v-if="status === 'active'">Active</h3>
  <h3 v-else-if="status === 'pending'">User is pending</h3>
  <h3 v-else>User is inactive</h3>

  <h3>Tasks:</h3>
  <ul>
    <li v-for="task in tasks" :key="task">{{ task }}</li>
  </ul>
  <!-- <a v-bind:href="bind">Google</a> -->
  <a :href="bind">Google</a>
  <!-- <button v-on:click="toggleStatus">Clicked me to toggle</button> -->
  <button @click="toggleStatus">Clicked me to toggle</button>
</template>
