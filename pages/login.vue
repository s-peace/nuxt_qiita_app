<template>
  <div>
    <h2>login page</h2>
    <p>
      <button type="button" @click="login">login</button>
      <br>
      <nuxt-link to="/">go to top page</nuxt-link>
    </p>
  </div>
</template>

<script>
import Cookies from 'universal-cookie'
export default {
  methods: {
    login(){
      const cookies = new Cookies()
      cookies.set('credential','true',{maxAge:90})
      this.$router.push('/')
    }
  }
}
</script>
