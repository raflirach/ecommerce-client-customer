<template>
  <div class="card col-2 m-1">
    <img :src="product.image_url" class="card-img-top" alt="...">
    <div class="">
      <p class="card-title">{{ product.name }}</p>
      <div class="footer">
        <div class="price">{{ price }}</div>
        <button
          @click.prevent="addToCart"
          class="btn btn-sm btn-primary"
        ><i class="fas fa-cart-plus"></i> add to cart</button>
      </div>
    </div>
  </div>
</template>

<script>
// import Swal from 'sweetalert2'

export default {
  name: 'ProductCard',
  props: ['product'],
  computed: {
    Toast () {
      return this.$store.state.Toast
    },
    price () {
      return this.product.price.toLocaleString('id', { style: 'currency', currency: 'IDR' })
    }
  },
  methods: {
    addToCart () {
      this.$store.dispatch('addToCart', this.product.id)
    }
  }
}
</script>

<style scoped>
  .card{
    padding: 0 !important;
    height: 280px;
    border: 1px solid #e3e3e3;
  }
  .card button{
    display: none;
    transform: translate(-6px, 23px);
    z-index: 100;
    width: 101.5%;
    position: absolute;
    border: 1.5px 1.5px 0 1.5px solid blue;
    border-top-left-radius: 0%;
    border-top-right-radius: 0%;
  }
  .card:hover{
    border: 1.5px solid blue;
  }
  .card:hover button{
    display: block;
  }
  img{
    width: 100%;
    height: 200px !important;
    object-fit: cover;
  }
  .footer{
    display: flex;
    justify-content: space-between;
    align-items: center;
    position: absolute;
    bottom: 0;
    width: 100%;
    padding-left: 5px;
  }
  .price{
    font-size: 0.9em;
  }
</style>
