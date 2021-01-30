<template>
  <div class="px-5">
    <div v-if="isLoading" class="d-flex justify-content-center">
      <lottie-player src="https://assets10.lottiefiles.com/packages/lf20_95DxC2.json"  background="transparent"  speed="1"  style="width: 300px; height: 300px;"  loop  autoplay></lottie-player>
    </div>
    <template v-if="!isLoading">
      <table class="table" v-if="transactions.length > 0">
        <tr>
          <th class="text-start" width="40%">Product</th>
          <th>Purchase Date</th>
          <th>Price</th>
          <th>Amount</th>
          <th>Total</th>
        </tr>
        <history-card
          v-for="transaction in transactions"
          :key="transaction.id"
          :transaction="transaction"
        />
      </table>
      <div v-else>
        <div class="fs-3">History empty</div>
        <button class="btn btn-outline-success" @click="$router.push('/')">Buy Now</button>
      </div>
    </template>
  </div>
</template>

<script>
import HistoryCard from '../components/HistoryCard.vue'
export default {
  components: { HistoryCard },
  name: 'History',
  data () {
    return {
      isLoading: true
    }
  },
  methods: {
    fetchTransaction () {
      this.isLoading = true
      this.$store.dispatch('fetchTransaction')
        .then(({ data }) => {
          this.$store.commit('insertCategory', data)
        })
        .catch(err => {
          console.log(err)
        })
        .finally(() => {
          this.isLoading = false
        })
    }
  },
  computed: {
    transactions () {
      return this.$store.state.transactions
    }
  },
  created () {
    setTimeout(() => {
      this.fetchTransaction()
    }, 500)
  },
  beforeRouteEnter (to, from, next) {
    if (to.path === '/history' && !localStorage.access_token) next({ name: 'Login' })
    else next()
  }
}
</script>

<style scoped>
  tr{
    border-bottom: 1px solid #e3e3e3;
  }
</style>
