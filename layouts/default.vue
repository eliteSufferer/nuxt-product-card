<template>
  <div class="layout">
    <AppHeader />
    <main class="main">
      <Nuxt />
    </main>
  </div>
</template>

<script>
export default {
  name: 'DefaultLayout'
}
</script>

<style scoped>
.layout {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}

.main {
  flex: 1;
  padding-top: 86px;
}

@media (max-width: 768px) {
  .main {
    padding-top: 60px;
  }
}
</style>