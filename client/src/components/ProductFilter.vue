<template>
  <div class='container'>
    <div class="mb-5">
      <h1>Product List</h1>
      <b-alert :variant="color" show v-if="notification[0]">{{notification[0]}}</b-alert>
    </div>
    <div class="products">
      <Product class="mb-3"
        v-for="product in products"
        :key= 'product.id'
        :product='product'
      >
      </Product>
    </div>
  </div>
</template>

<script>
import Product from '../components/ProductItem'
export default {
  components: {
    Product
  },
  computed: {
    products: {
      get () {
        return this.$store.state.productsFilter
      }
    },
    notification: {
      get () {
        return this.$store.state.notification
      }
    },
    color: {
      get () {
        return this.$store.state.color
      }
    }
  },
  created () {
    this.$store.dispatch('fetchProductsFilter', this.$route.params.filter)
  }
}
</script>

<style>
.container {
  display: flex;
  flex-direction: column;
}
.products {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
}

</style>
