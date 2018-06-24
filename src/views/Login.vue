<template>
  <v-container>
    <v-layout>
      <v-flex>
        <v-card>
          <v-card-text>
            <v-form ref="formLogin" @submit="entrar">
              <v-text-field
                label="Usuário"
                v-model="usuario"
                :rules="[validacoes.obrigatorio]"
                @keyup.enter="entrar"
              ></v-text-field>
              <v-text-field
                label="Senha"
                v-model="senha"
                type="password"
                :rules="[validacoes.obrigatorio]"
                @keyup.enter="entrar"
              ></v-text-field>
            </v-form>
          </v-card-text>
          <v-card-actions>
            <v-btn color="primary" @click="entrar">Entrar</v-btn>
          </v-card-actions>
        </v-card>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
  import jwt from 'jsonwebtoken'

  export default {
    data: () => ({
      usuario: '',
      senha: '',
      validacoes: {
        obrigatorio: v => !!v || 'Esse campo é obrigatório!'
      }
    }),
    methods: {
      entrar() {
        if (this.$refs.formLogin.validate()) {
          jwt.sign({
            usuario: this.usuario,
            senha: this.senha
          }, 'palavraChaveJwt', (err, token) => {
            window.localStorage.setItem('token', token)
            this.$router.push('/')
          })
        }
      }
    }
  }
</script>