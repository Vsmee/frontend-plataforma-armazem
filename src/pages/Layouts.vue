<template>
  <DefaultLayout>
    <template #default>
      <v-container>
        <v-row align="center" justify="space-between" class="mb-4">
          <h1 class="text-h5">Meus Layouts</h1>
          <v-btn color="primary" @click="dialog = true">Novo layout</v-btn>
        </v-row>

        <v-alert type="info" v-if="layouts.length === 0">
          Nenhum layout cadastrado.
        </v-alert>

        <v-row>
          <v-col
            v-for="layout in layouts"
            :key="layout.id"
            cols="12"
            md="4"
          >
            <v-card>
              <v-card-title>{{ layout.nome }}</v-card-title>
              <v-card-subtitle>{{ formatDate(layout.criado_em) }}</v-card-subtitle>
              <v-card-actions>
                <v-btn color="error" @click="deletarLayout(layout.id)">Excluir</v-btn>
              </v-card-actions>
            </v-card>
          </v-col>
        </v-row>

        <!-- Diálogo de novo layout -->
        <v-dialog v-model="dialog" max-width="400">
          <v-card>
            <v-card-title>Criar Layout</v-card-title>
            <v-card-text>
              <v-text-field label="Nome do layout" v-model="novoNome" />
            </v-card-text>
            <v-card-actions>
              <v-spacer />
              <v-btn color="grey" text @click="dialog = false">Cancelar</v-btn>
              <v-btn color="primary" @click="criarLayout">Salvar</v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </v-container>
    </template>
  </DefaultLayout>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import DefaultLayout from '@/layouts/DefaultLayout.vue'
import api from '@/services/api'

const layouts = ref([])
const dialog = ref(false)
const novoNome = ref('')

// Buscar layouts ao carregar
const carregarLayouts = async () => {
  try {
    const response = await api.get('/layouts')
    layouts.value = response.data
  } catch (error) {
    console.error('Erro ao carregar layouts:', error)
  }
}

onMounted(carregarLayouts)

// Criar novo layout
const criarLayout = async () => {
  if (!novoNome.value) return

  try {
    await api.post('/layouts', { nome: novoNome.value })
    dialog.value = false
    novoNome.value = ''
    carregarLayouts()
  } catch (error) {
    console.error('Erro ao criar layout:', error)
  }
}

// Deletar layout
const deletarLayout = async (id) => {
  try {
    await api.delete(`/layouts/${id}`)
    carregarLayouts()
  } catch (error) {
    console.error('Erro ao deletar layout:', error)
  }
}

// Formatar data
const formatDate = (data) => {
  return new Date(data).toLocaleString('pt-BR')
}
</script>
