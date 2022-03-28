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
// $('#myModal').on('shown.bs.modal', function () {
//   $('#myInput').trigger('focus')
// })

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


<div class="modal fade" id="exampleModal" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
  <div class="modal-dialog" role="document">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title" id="exampleModalLabel">New message</h5>
        <button type="button" class="close" data-dismiss="modal" aria-label="Close">
          <span aria-hidden="true">&times;</span>
        </button>
      </div>
      <div class="modal-body">
        <form>
          <div class="form-group">
            <label for="recipient-name" class="">Recipient:</label>
            <input type="text" class="form-control" id="recipient-name">
          </div>
          <div class="form-group">
            <label for="message-text" class="col-form-label">Message:</label>
            <input type="text" class="form-control" id="recipient-name">
          </div>
        </form>
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
        <button type="submit" class="btn btn-primary">Update</button>
      </div>
    </div>
  </div>
  </div>
  <tr v-for="user in users" :key="user.id">
    <th scope="col">{{user.id}}</th>
    <th scope="col">{{ user.name }}</th>
    <th scope="col">{{ user.email }}</th>
    <th scope="col">{{ user.role }}</th>
    <th scope="col" :class="user.inactive?'in':'ac'"><span>
      </span>{{ user.inactive? "Inactive" : "Active" }}</th>
    <th scope="col"> <button @click="updateRow(user.id)" >Edit</button> <button @click="deleteRow(user.id)"
   >{{user.inactive? "Undo" : "Delete"}} </button> </th>
   <th><button type="button" class="btn btn-primary" data-toggle="modal" data-target="#exampleModal" data-whatever="@mdo">Edit</button></th>
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
.in{
  color: red;
}
.ac{
  color: green;
}
.card-body {
  background-color: rgb(94, 217, 255);
}
</style>
