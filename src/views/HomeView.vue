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
              placeholder="Type keyword to search, e.g. Leanne"
              aria-label="Search"
              v-model="search"
              @keyup.enter="searchUser">
          </div>
        </div>

        <div class="row mt-3">
          <div class="col">
            <label class="form-label d-block">Search by</label>
            <div class="form-check form-check-inline">
              <input class="form-check-input" type="checkbox" id="inlineCheckbox1" value="name" v-model="searchBy">
              <label class="form-check-label" for="inlineCheckbox1">Name</label>
            </div>
            <div class="form-check form-check-inline">
              <input class="form-check-input" type="checkbox" id="inlineCheckbox2" value="username" v-model="searchBy">
              <label class="form-check-label" for="inlineCheckbox2">Username</label>
            </div>
            <div class="form-check form-check-inline">
              <input class="form-check-input" type="checkbox" id="inlineCheckbox3" value="email" v-model="searchBy">
              <label class="form-check-label" for="inlineCheckbox3">Email</label>
            </div>
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
        searchBy: [],
        search: ''
      }
    },

    mounted() {
      this.getUsers()
    },

    methods: {
      searchUser() {
        this.getUsers()
      },
      getUsers() {
        axios.get(import.meta.env.VITE_API_URL)
          .then(({data}) => {
            const result = data.data
            if (this.search && this.searchBy.length) {
              this.users = this.filterResult(result)
            } else {
              this.users = result
            }
          })
          .catch((error) => {
            console.log(error)
            alert('Failed to load data')
          })
      },
      filterResult(result) {
        const users = []
        result.forEach((user) => {
          this.searchBy.forEach((searchKey) => {
            const value = user[searchKey].toLowerCase()
            if (value.indexOf(this.search) != -1) {
              users.push(user)
            }
          })
        })
        return users
      }
    },
  }
</script>