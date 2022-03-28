<script setup>
import { ref } from 'vue';

defineProps({
  id: Number,
  name: String,
  email: String,
  role: String,
  status: String,
});


</script>

<template>
  <tr>
    <th scope="col">{{ id }}</th>
    <th scope="col">{{ name }}</th>
    <th scope="col">{{ email }}</th>
    <th scope="col">{{ role }}</th>
    <th scope="col">{{ status }}</th>
    <th scope="col"> <button >Edit</button> <button>Delete</button> </th>
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
