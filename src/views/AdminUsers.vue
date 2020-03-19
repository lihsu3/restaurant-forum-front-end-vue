<template>
  <div class="container py-5">
    <AdminNav />

    <table class="table">
      <thead class="thead-dark">
        <tr>
          <th scope="col">
            #
          </th>
          <th scope="col">
            Email
          </th>
          <th scope="col">
            Role
          </th>
          <th
            scope="col"
            width="140"
          >
            Action
          </th>
        </tr>
      </thead>
      <tbody>

        <tr
          v-for="user in users"
          :key="user.id"
        >
          <th scope="row">
            {{ user.id }}
          </th>
          <td>{{ user.email }}</td>
          <td v-if="user.isAdmin">admin</td>
          <td v-else>user</td>
          <td>
            <button
              v-show="currentUser.id !== user.id"
              v-if="user.isAdmin"
              type="button"
              class="btn btn-link"
              @click.stop.prevent="toggleUserRole(user.id)"
            >
              set as user
            </button>
            <button
              v-show="currentUser.id !== user.id"
              v-else
              type="button"
              class="btn btn-link"
              @click.stop.prevent="toggleUserRole(user.id)"
            >
              set as admin
            </button>
          </td>
        </tr>

      </tbody>
    </table>
  </div>
</template>

<script>
import AdminNav from '../components/AdminNav.vue'

const dummyUser = {
  currentUser: {
    id: 1,
    name: '管理者',
    email: 'root@example.com',
    image: 'https://i.pravatar.cc/300',
    isAdmin: true
  },
  isAuthenticated: true
}

const dummyData = {
  "users": [
    {
      "id": 1,
      "name": "root",
      "email": "root@example.com",
      "password": "$2a$10$J9pLpJJ1Tzfe/ZcjdYwXdumyh.3F5E.w/HTxRcH./cl3azhgekgQe",
      "isAdmin": true,
      "image": null,
      "createdAt": "2020-02-28T14:38:32.000Z",
      "updatedAt": "2020-03-02T17:09:40.000Z"
    },
    {
      "id": 2,
      "name": "user1",
      "email": "user1@example.com",
      "password": "$2a$10$J9pLpJJ1Tzfe/ZcjdYwXdumyh.3F5E.w/HTxRcH./cl3azhgekgQe",
      "isAdmin": false,
      "image": null,
      "createdAt": "2020-02-28T14:38:32.000Z",
      "updatedAt": "2020-03-02T17:09:40.000Z"
    },
  ]
}

export default {
  components: {
    AdminNav
  },
  data () {
    return {
      users: [],
      currentUser: dummyUser.currentUser
    }
  },
  created () {
    this.fetchUsers()
  },
  methods: {
    fetchUsers () {
      this.users = dummyData.users
    },
    toggleUserRole (userId) {
      //back end

      this.users = this.users.map((user) => {
        if (user.id === userId) {
          return {
            ...user,
            isAdmin: !user.isAdmin
          }
        }
        return user
      })
    }
  }
}
</script>
