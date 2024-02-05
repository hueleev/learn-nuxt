<template>
  <div>
    <header class="title">
      <NuxtLink class="logo" to="/">Nuxt Shopping</NuxtLink>
      <!-- <h1>{{ $route.name }} 페이지</h1> -->
      <!-- router-link -->
      <!-- <NuxtLink to="/">홈페이지</NuxtLink>
      <NuxtLink to="/main">메인</NuxtLink>
      <NuxtLink to="/product">상품</NuxtLink> -->
    </header>
    <!-- router-view -->
    <Nuxt />
  </div>
</template>

<script>
export default {}
</script>

<style scoped>
header {
  height: 60px;
  display: flex;
  align-items: center;
  padding: 0 0.5rem;
}
.logo {
  font-weight: 900;
}
.logo:visited {
  color: inherit;
}
</style>
