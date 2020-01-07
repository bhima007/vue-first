<template>
  <div class="hello">
    <p>Hello World</p>
    <p>the id is {{ id }}.</p>
    <div class="identity">
      <span>{{ user.name }}</span>
      <hr>
      <span>{{ user.username }}</span>
      <span>{{ user.email }}</span>
      <span>{{ user.website }}</span>
      <span>{{ user.phone }}</span>
    </div>
    <br>
    <br>
    <div>
      <button @click="previousUser" v-if="id != 1">Previous</button>
      <button @click="nextUser" v-if="id != 10">Next</button>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'HelloWorld',
  data () {
    return {
      id: this.$route.params.id,
      user: ''
    }
  },
  created () {
    this.getUser()
  },
  watch: {
    id () {
      this.$router.push(`/about/${this.id}`);
      this.getUser()
      console.log(this.$route.params.id)
    }
  },
  methods: {
    getUser () {
      axios.get(`https://jsonplaceholder.typicode.com/users/${this.id}`)
        .then(res => {
          this.user = res.data
        })
        .catch(error => console.log('error', error))
    },
    previousUser () {
      this.id--
    },
    nextUser () {
      this.id++
    }
  }
}
</script>

<style scoped>
  .identity {
    display: flex;
    flex-direction: column;
  }
</style>
