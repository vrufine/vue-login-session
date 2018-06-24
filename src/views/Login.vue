<template>
  <div class="about">
    <form @submit="entrar($event)">
      <input type="text" v-model="usuario" required>
      <input type="password" v-model="senha" required>
      <button type="submit" @click="entrar">Entrar</button>
    </form>
  </div>
</template>

<script>
  import jwt from 'jsonwebtoken'
  export default {
    data: () => ({
      usuario: '',
      senha: ''
    }),
    methods: {
      async entrar(event) {
        event.preventDefault()
        const token = await jwt.sign(JSON.stringify({
          usuario: this.usuario
        }), 'senha_secreta')
        window.localStorage.setItem('tokenLogado', token)
        this.$router.push('/')
      }
    }
  }
</script>

<style scoped>
  input {
    display: block;
  }
</style>