<template>
  <v-container fill-height>
    <v-layout>
      <v-flex>
        <h1>Página inicial</h1>
      </v-flex>
    </v-layout>
    <v-layout>
      <v-flex v-if="logado">
        Usuário logado: <strong>{{ usuarioLogado.usuario }}</strong>
        <v-btn @click="logout">Sair</v-btn>
      </v-flex>
      <v-flex v-else>
        <v-btn to="/login">Entrar</v-btn>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
  export default {
    data: () => ({
      logado: false,
    }),
    methods: {
      isLogado() {
        window.localStorage.getItem('token')
          ? this.logado = true
          : this.logado = false
      },
      logout() {
        window.localStorage.removeItem('token')
        this.$router.push('/login')
      }
    },
    computed: {
      usuarioLogado() {
        const token = window.localStorage.getItem('token')
        const payload = JSON.parse(atob(token.split('.')[1]))
        return payload
      }
    },
    mounted() {
      this.isLogado()
    }
  }
</script>