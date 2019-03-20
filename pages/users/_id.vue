<template>
  <div>
    <p>
      <h3>{{user.id}}</h3>
      <img :src="user.profile_image_url" width="120" alt="">
      <p>{{user.description || 'No description'}}</p>
      <p>
        <nuxt-link to="/">
          <small>go back to Top</small>
        </nuxt-link>
      </p>
      <h3>{{user.id}} s posts list</h3>
      <ul>
        <li v-for="item in items" :key="item.id">
          <h4>
            <span>{{item.title}}</span>
          </h4>
          <div>{{item.body.slice(0,130)}}.....</div>
          <p><a target="_blank" :href="item.url">{{item.url}}</a></p>
        </li>
      </ul>
  </div>
</template>

<script>
import {mapGetters} from 'vuex'

export default {
  head() {
    return {
      title: this.user.id
    }
  },
  async asyncData({route,store,redirect}){
    if(store.getters['users']['route.params.id']){
      return
    }
    try {
      await store.dispatch('fetchUserInfo',{id: route.params.id})
    } catch(e) {
      redirect('/')
    }
    // const user = await app.$axios.$get(`https://qiita.com/api/v2/users/${route.params.id}`)
    // const items = 
    //   await app.$axios.$get(`https://qiita.com/api/v2/items?query=user:${route.params.id}`)
    // return {user,items}
  },
  computed: {
    user() {
      return this.users[this.$route.params.id]
    },
    items() {
      return this.userItems[this.$route.prams.id] || []
    },
    ...mapGetters(['users','userItems'])
  }
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}
h3 {
  margin: 16px 0;
  padding: 8px 0;
  border-bottom: 1px solid #e5e5e5;
}
li + li {
  margin: 16px 0;
}
p {
  margin: 8px 0;
}
</style>
