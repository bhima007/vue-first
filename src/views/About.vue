<template>
  <div class="about">
    <h1>This is an about page</h1>
    <ListPosts :posts="posts"/>
  </div>
</template>

<script>
import axios from 'axios'
import ListPosts from '@/components/ListPosts.vue'

export default {
  components: {
    ListPosts
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