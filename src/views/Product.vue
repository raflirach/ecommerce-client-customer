<template>
  <div class="container">
    <s-slider v-if="isBannerLoading"/>
    <slider v-else></slider>
    <div class="row d-flex justify-content-center">
      <template v-if="isProductLoading">
        <s-product v-for="(item,i) in 10" :key="1e6+i"/>
      </template>
      <template v-else>
        <div v-if="products.length < 1" class="fs-3">No Product Available</div>
        <product-card
          v-for="product in products"
          :key="product.id"
          :product="product"
        />
      </template>
    </div>
  </div>
</template>

<script>
import ProductCard from '../components/ProductCard.vue'
import Slider from '../components/Slider.vue'
import SProduct from '../components/Skeleton/SProduct'
import SSlider from '../components/Skeleton/SSlider.vue'

export default {
  components: { ProductCard, Slider, SProduct, SSlider },
  name: 'Product',
  data () {
    return {
      isProductLoading: true,
      isBannerLoading: true
    }
  },
  methods: {
    fetchProduct () {
      this.isProductLoading = true
      this.$store.dispatch('fetchProduct')
        .then(({ data }) => {
          this.$store.commit('insertProduct', data)
        })
        .catch(err => {
          console.log(err)
        })
        .finally(() => { this.isProductLoading = false })
    },
    fetchBanner () {
      this.isBannerLoading = true
      this.$store.dispatch('fetchBanner')
        .then(({ data }) => {
          this.$store.commit('insertBanner', data)
        })
        .catch(err => {
          console.log(err)
        })
        .finally(() => { this.isBannerLoading = false })
    }
  },
  computed: {
    products () {
      return this.$store.getters.filterProducts
    },
    filter () {
      return this.$store.state.filter
    },
    categories () {
      return this.$store.state.categories
    }
  },
  created () {
    this.fetchProduct()
    this.fetchBanner()
  }
}
</script>

<style scoped>

</style>
