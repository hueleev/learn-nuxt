<template>
  <div></div>
</template>

<script>
import { fetchProducts } from '@/api'

export default {
  async asyncData() {
    const response = await fetchProducts()
    const products = response.data
    return { products }
  },
}
</script>

<style lang="scss" scoped></style>
