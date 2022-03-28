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

import axios from 'axios';

export default {
  data() {
    return {
      users: [],
      errors: []
    }
  },
  methods: {
  async deleteRow(id) {
    try {
        var curr_status = this.users[id].inactive
        await axios.patch(`${`http://localhost:3000/users`}/${id}`, {
            inactive: !curr_status
        });
        this.users = this.users.map(user => {
            if (user.id === id) {
                user.inactive = !user.inactive;
            }
            //console.log(user)
            return user;

        });
    } catch (error) {
        console.error(error);
    }
},
async updateRow(id){
  var Name = prompt("Name",this.users[id].name);
  var Email = prompt("Email",this.users[id].email);
  var Role = prompt("Role",this.users[id].role);
  try {
        var curr_status = this.users[id].inactive
        await axios.patch(`${`http://localhost:3000/users`}/${id}`, {
            name: Name,
            email: Email,
            role: Role,
        });
        this.users = this.users.map(user => {
            if (user.id === id) {
                user.name = Name;
                user.email = Email;
                user.role = Role;
            }
            //console.log(user)
            return user;

        });
    } catch (error) {
        console.error(error);
    }
}

  },

  // Fetches posts when the component is created.
  async created() {
    try {
      const response = await axios.get(`http://localhost:3000/users`)
      this.users = response.data
      //console.log(this.users)
    } catch (e) {
      this.errors.push(e)
    }
  }
}

</script>

<template>
  <tr v-for="user in users" :key="user.id">
    <th scope="col">{{user.id}}</th>
    <th scope="col">{{ user.name }}</th>
    <th scope="col">{{ user.email }}</th>
    <th scope="col">{{ user.role }}</th>
    <th scope="col">{{ user.inactive? "Inactive" : "Active" }}</th>
    <th scope="col"> <button @click="updateRow(user.id)" >Edit</button> <button @click="deleteRow(user.id)"
   >{{user.inactive? "Undo" : "Delete"}} </button> </th>
  </tr>
</template>

<style scoped>
a {
  color: #42b983;
}

.btn-disabled{
    cursor: not-allowed;
    pointer-events: none;
}

.card-body {
  background-color: rgb(94, 217, 255);
}
</style>
