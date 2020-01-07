<template>
  <div class="about">
    <h1>This is an about page</h1>
    <ListUsers :users="users"/>
    <button @click="navigateToPage('/about')">About</button>
    <button @click="navigateToPage('/about/posts')">Posts</button>
    <router-view />
  </div>
</template>

<script>
import axios from 'axios'
import ListUsers from '@/components/ListUsers.vue'

export default {
  components: {
    ListUsers
  },
  data () {
    return {
      users: []
    }
  },
  created () {
    axios.get('https://jsonplaceholder.typicode.com/users')
      .then(res => {
        this.users = res.data
      })
      .catch(error => console.log('error', error))
  },
  methods: {
    navigateToPage (par) {
      this.$router.push(par)
    }
  }
}
</script>