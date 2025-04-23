<template>
  <v-app id="inspire">
    <!-- Barra lateral -->
    <v-navigation-drawer v-model="drawer">
      <v-list nav>
        <v-list-item title="Home" to="/home" />
        <v-list-item title="Layouts" to="/layouts" />
        <v-list-item title="Produtos" to="/produtos" />
      </v-list>
    </v-navigation-drawer>

    <!-- Cabeçalho -->
    <v-app-bar>
      <v-app-bar-nav-icon @click="drawer = !drawer" />
      <v-app-bar-title>Plataforma de Armazém</v-app-bar-title>
      <v-spacer />
      <v-btn icon @click="logout">
        <v-icon>mdi-logout</v-icon>
      </v-btn>
    </v-app-bar>

    <!-- Conteúdo da página -->
    <v-main class="pa-4">
      <slot />
    </v-main>

  </v-app>
</template>

<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'

const drawer = ref(true)
const router = useRouter()

const logout = () => {
  localStorage.removeItem('token')
  router.push('/login')
}
</script>
