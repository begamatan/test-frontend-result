<template>
  <div class="card my-3">
    <div class="card-body">
      <table class="table table-default">
        <tbody>
          <tr>
            <td class="fw-bold">Name</td>
            <td>{{ user.name }}</td>
          </tr>
          <tr>
            <td class="fw-bold">User Name</td>
            <td>{{ user.username }}</td>
          </tr>
          <tr>
            <td class="fw-bold">Email</td>
            <td>{{ user.email }}</td>
          </tr>
          <tr>
            <td class="fw-bold">Address</td>
            <td>{{ fullAddress }}</td>
          </tr>
          <tr>
            <td class="fw-bold">Phone</td>
            <td>{{ user.phone }}</td>
          </tr>
          <tr>
            <td class="fw-bold">Website</td>
            <td>{{ user.website }}</td>
          </tr>
          <tr>
            <td class="fw-bold">Company</td>
            <td>{{ user.company.name }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'UserCard',

    props: {
      user: {
        type: Object,
        required: true
      }
    },

    computed: {
      fullAddress() {
        const address = this.user.address
        return `${address.street}, ${address.suite}, ${address.city}, ${address.zipcode}`
      }
    }
  }
</script>