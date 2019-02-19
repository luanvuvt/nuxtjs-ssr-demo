<template>
  <section class="container">
    <div>
      <h1 class="title">Users</h1>
      <ul>
        <li v-for="user in users" :key="user.id">{{ user.first_name }}</li>
      </ul>
      <nuxt-link to="?page=1">1</nuxt-link>
      <nuxt-link to="?page=2">2</nuxt-link>
      <nuxt-link to="?page=3">3</nuxt-link>
      <nuxt-link to="?page=4">4</nuxt-link>
    </div>
  </section>
</template>

<script>
import { mapState } from 'vuex'

export default {
  async fetch({ $axios, store, query }) {
    const page = query.page ? query.page : 1
    const { data } = await $axios.get(`https://reqres.in/api/users?page=${page}`)
    store.commit('setUsers', data.data)
  },
  computed: mapState([
    'users'
  ]),
  watchQuery: ['page']
}
</script>
