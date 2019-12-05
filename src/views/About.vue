<template>
  <div class="about">
    <h1>This is an about page</h1>
    <ListUsers :posts="posts"/>
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
      posts: []
    }
  },
  created () {
    axios.get('https://jsonplaceholder.typicode.com/posts')
      .then(res => {
        this.posts = res.data
      })
      .catch(error => console.log('error', error))
  }
  }
</script>