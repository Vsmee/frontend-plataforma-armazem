<template>
  <v-container class="d-flex justify-center align-center fill-height">
    <v-card width="400" class="pa-6">
      <v-card-title class="text-h6 text-center">Login</v-card-title>

      <v-form @submit.prevent="handleLogin">
        <v-text-field
          v-model="email"
          label="Email"
          type="email"
          required
        ></v-text-field>

        <v-text-field
          v-model="senha"
          label="Senha"
          type="password"
          required
        ></v-text-field>

        <v-btn type="submit" color="primary" class="mt-4" block>Entrar</v-btn>

        <v-alert
          v-if="erro"
          type="error"
          class="mt-3"
          dense
          text
        >
          {{ erro }}
        </v-alert>
      </v-form>
    </v-card>
  </v-container>
</template>

<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'
import api from '@/services/api'

const email = ref('')
const senha = ref('')
const erro = ref('')
const router = useRouter()

const handleLogin = async () => {
  erro.value = ''

  try {
    const response = await api.post('/login', {
      email: email.value,
      senha: senha.value
    })

    const token = response.data.token
    localStorage.setItem('token', token)

    router.push('/Home')
  } catch (err) {
    erro.value = 'Email ou senha inválidos'
    console.error(err)
  }
}
</script>
