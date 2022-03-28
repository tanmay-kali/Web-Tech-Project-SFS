<script>
// import { ref } from 'vue';
// import axios from 'axios';

// defineProps({
//   id: String,
//   name: String,
//   email: String,
//   role: String,
//   status: String,
// });

import axios from "axios";

export default {
  data() {
    return {
      users: [],
      errors: [],
    };
  },
  // Fetches posts when the component is created.
  async created() {
    try {
      const response = await axios.get("http://localhost:3004/users");
      this.users = response.data;
      console.log(this.users);
    } catch (e) {
      this.errors.push(e);
    }
  },
};
</script>

<template>
  <tr v-for="user in users" :key="user.id">
    <th scope="col">{{user.id}}</th>
    <th scope="col">{{ user.name }}</th>
    <th scope="col">{{ user.email }}</th>
    <th scope="col">{{ user.role }}</th>
    <th scope="col">{{ user.inactive? "Inactive" : "Active" }}</th>
    <th scope="col"> <button >Edit</button> <button 
    @click="deleterow()">{{user.inactive? "Undo" : "Delete"}} </button> </th>
  </tr>
</template>

<style scoped>
a {
  color: #42b983;
}

.card-body {
  background-color: rgb(94, 217, 255);
}
</style>
