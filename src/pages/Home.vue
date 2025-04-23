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

const backgroundStyle = {
  backgroundImage: `url(${new URL('@/assets/Liv.jpg', import.meta.url).href})`,
  backgroundSize: 'cover',
  backgroundPosition: 'center',
  height: 'calc(100vh - 64px)',
  display: 'flex',
  alignItems: 'center',
  justifyContent: 'center',
  color: 'white'
}
</script>


<style scoped>
.content {
  background-color: rgba(0, 0, 0, 0.5);
  padding: 2rem;
  border-radius: 8px;
  text-align: center;
}
</style>

