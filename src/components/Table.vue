<script setup>
import { ref } from 'vue';
import Rows from './Rows.vue';
</script>

<template>
  <body>
    <div class="container">
      <div class="card">
        <div class="card-body">
          <h5 class="card-title">User Management</h5>
          <button type="button" class="btn btn-primary">Add User</button>
        </div>
      </div>
      <table class="table">
        <thead>
          <tr>
            <th scope="col">ID</th>
            <th scope="col">Name</th>
            <th scope="col">Email</th>
            <th scope="col">Role</th>
            <th scope="col">Status</th>
            <th scope="col">Actions</th>
          </tr>
        </thead>
        <tbody id="userTableBody">
          <Rows></Rows>
        </tbody>
      </table>
    </div>
  </body>
</template>

<style scoped>
a {
  color: #42b983;
}

.card-body {
  background-color: rgb(94, 217, 255);
}
</style>
