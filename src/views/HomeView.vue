<template>
  <div class="container">
    <div class="row my-3">
      <div class="col col-sm-4">
        <div class="row">
          <div class="col">
            <label class="form-label">Search</label>
            <input
              type="search"
              class="form-control"
              placeholder="Type keyword to search, e.g. leanne"
              aria-label="Search"
              v-model="search"
              @keyup.enter="searchUser">
          </div>
        </div>

        <div class="row mt-3">
          <div class="col">
            <button @click="searchUser" type="button" class="btn btn-primary">Search</button>
          </div>
        </div>
      </div>
    </div>
    <div class="row">
      <div class="col col-sm-4" v-for="user in users" :key="user.id">
        <user-card :user="user" />
      </div>
    </div>
  </div>
</template>

<script>
  import axios from 'axios'
  import UserCard from '../components/UserCard.vue'

  export default {
    components: {
      UserCard
    },

    data() {
      return {
        users: [],
        search: '',
        filter: ['name', 'username', 'email']
      }
    },

    mounted() {
      this.getUsers()
    },

    methods: {
      searchUser() {
        this.filterUser()
      },
      getUsers() {
        axios.get(import.meta.env.VITE_API_URL)
          .then(({data}) => {
            this.users = data.data
          })
          .catch((error) => {
            console.log(error)
            alert('Failed to load data')
          })
      },
      filterUser() {
        if (!this.search) {
          return this.getUsers()
        }
        const users = []
        this.users.forEach((user) => {
          this.filter.forEach((searchKey) => {
            const value = user[searchKey].toLowerCase()
            if (value.indexOf(this.search) != -1) {
              users.push(user)
            }
          })
        })
        this.users = users
      }
    },
  }
</script>