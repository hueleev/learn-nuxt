<template>
  <div class="app">
    <main>
      <SearchInput v-model="searchKeyword" @search="searchProducts" />
      <!-- :search-keyword="searchKeyword"
        @input="updateSearchKeyword" -->
      <ul>
        <li
          v-for="product in products"
          :key="product.id"
          class="item flex"
          @click="moveToDetailPage(product.id)"
        >
          <img class="product-image" :src="product.imageUrl" alt="" />
          <p>{{ product.name }}</p>
          <span>{{ product.price }}</span>
        </li>
      </ul>
      <div class="cart-wrapper">
        <button class="btn" @click="moveToCartPage">장바구니</button>
      </div>
    </main>
  </div>
</template>

<script>
import axios from 'axios'
import { fetchProductsByKeyword } from '@/api/index'
import SearchInput from '@/components/SearchInput.vue'

export default {
  components: { SearchInput },
  async asyncData() {
    const response = await axios.get('http://localhost:3000/products')
    const products = response.data.map((item) => ({
      ...item,
      imageUrl: `${item.imageUrl}?random=${Math.random()}`,
    }))
    return { products }
  },
  data() {
    return {
      searchKeyword: '',
    }
  },
  methods: {
    moveToDetailPage(id) {
      this.$router.push(`detail/${id}`) // detail 디렉토리에 _id.vue 로 라우팅됨.
    },
    // updateSearchKeyword(keyword) {
    //   this.searchKeyword = keyword
    // },
    async searchProducts() {
      const response = await fetchProductsByKeyword(this.searchKeyword)
      this.products = response.data
    },
    moveToCartPage() {
      this.$router.push('/cart')
    },
  },
}
</script>

<style scoped>
.flex {
  display: flex;
  justify-content: center;
}

.item {
  display: inline-block;
  width: 400px;
  height: 300px;
  text-align: center;
  margin: 0 0.5rem;
  cursor: pointer;
}

.product-image {
  /* width:400px */
  width: 250px;
  height: 250px;
}

.app {
  position: relative;
}

.cart-wrapper {
  position: sticky;
  float: right;
  bottom: 50px;
  right: 50px;
}

.cart-wrapper .btn {
  display: inline-block;
  height: 40px;
  font-size: 1rem;
  font-weight: 500;
}
</style>
