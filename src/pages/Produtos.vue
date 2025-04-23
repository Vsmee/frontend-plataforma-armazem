<template>
  <DefaultLayout>
    <template #default>
      <div class="home-bg" :style="backgroundStyle">
        <div class="content">
          <h1 class="text-h4 font-weight-bold mb-4">Bem-vindo!</h1>
          <p class="text-subtitle-1">Gerencie seus layouts de forma simples e eficiente.</p>
        </div>
      </div>
    </template>
  </DefaultLayout>
</template>

<script setup>
import DefaultLayout from '@/layouts/DefaultLayout.vue'
</script>