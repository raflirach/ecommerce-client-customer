<template>
  <div>
    <div class="fs-3 mb-3">Login</div>
    <form @submit.prevent="login">
      <div class="mb-3 form-group">
        <label class="form-label">Email address</label>
        <input type="email" class="form-control" v-model="email" aria-describedby="emailHelp">
        <div id="emailHelp" class="form-text">We'll never share your email with anyone else.</div>
      </div>
      <div class="mb-3">
        <label class="form-label form-group">Password</label>
        <input type="password" class="form-control" v-model="password">
      </div>
      <div v-if="isError" class="alert alert-danger" role="alert">
        {{ isError }}
      </div>
      <button v-if="!isLoading" type="submit" class="btn btn-success">Log in</button>
      <div v-else class="btn btn-success"><span class="spinner-border spinner-border-sm"></span> Logging in</div>
    </form>
    <div class="mt-2">Not on R-commerce yet? <a href="" @click.prevent="navigateRegisterForm">Register</a></div>
  </div>
</template>

<script>
export default {
  name: 'Login',
  data () {
    return {
      email: '',
      password: '',
      isLoading: '',
      isError: ''
    }
  },
  methods: {
    navigateRegisterForm () {
      this.$router.push('/register')
    },
    login () {
      this.isLoading = true
      this.isError = ''
      const { email, password } = this
      const payload = { email, password }
      this.$store.dispatch('login', payload)
        .then(({ data }) => {
          localStorage.access_token = data.access_token
          this.$router.push('/')
        })
        .catch(err => {
          this.isError = err.response.data.message
        })
        .finally(() => {
          this.isLoading = false
        })
    }
  }
}
</script>

<style scoped>
  .form-group{
    display: flex;
    flex-direction: column;
    align-items: flex-start;
  }
</style>
