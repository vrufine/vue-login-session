<template>
  <v-container fill-height>
    <v-layout>
      <v-flex>
        <h1>Home page</h1>
      </v-flex>
    </v-layout>
    <v-layout>
      <v-flex v-if="logged">
        Active user: <strong>{{ loggedUser.user }}</strong>
        <v-btn @click="logout">Logout</v-btn>
      </v-flex>
      <v-flex v-else>
        <v-btn to="/login">Login</v-btn>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
  export default {
    data: () => ({
      logged: false,
    }),
    methods: {
      isLogged() {
        window.localStorage.getItem('token')
          ? this.logged = true
          : this.logged = false
      },
      logout() {
        window.localStorage.removeItem('token')
        this.$router.push('/login')
      }
    },
    computed: {
      loggedUser() {
        const token = window.localStorage.getItem('token')
        const payload = JSON.parse(atob(token.split('.')[1]))
        return payload
      }
    },
    mounted() {
      this.isLogged()
    }
  }
</script>