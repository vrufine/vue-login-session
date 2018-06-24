<template>
  <v-container>
    <v-layout>
      <v-flex>
        <v-card>
          <v-card-text>
            <v-form ref="formLogin" @submit="login">
              <v-text-field
                label="User"
                v-model="user"
                :rules="[validations.required]"
                @keyup.enter="login"
              ></v-text-field>
              <v-text-field
                label="Password"
                v-model="password"
                type="password"
                :rules="[validations.required]"
                @keyup.enter="login"
              ></v-text-field>
            </v-form>
          </v-card-text>
          <v-card-actions>
            <v-btn color="primary" @click="login">Login</v-btn>
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
      user: '',
      password: '',
      validations: {
        required: v => !!v || 'This is a required field!'
      }
    }),
    methods: {
      login() {
        if (this.$refs.formLogin.validate()) {
          jwt.sign({
            user: this.user,
            password: this.password
          }, 'jwtSecret', (err, token) => {
            window.localStorage.setItem('token', token)
            this.$router.push('/')
          })
        }
      }
    }
  }
</script>