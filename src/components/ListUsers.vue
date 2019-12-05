<template>
  <div class="box container">
    <div class="card-list" v-for="post in posts" :key="post.id">
      {{ post.title }}
    </div>
  </div>
</template>

<script>
export default {
  name: 'List',
  props: {
    posts: {
      type: Array
    }
  }
}
</script>

<style scoped>
table {
  width: 100%
}
tr {
  vertical-align: top;
}
td {
  width: 120px
}
.box {
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
}
.card-list {
  background: teal;
  width: 200px;
  height: 100px;
  margin: 8px;
  padding: 8px;
  color: aliceblue;
  cursor: pointer;
}
.card-list:hover {
  background: seagreen;
}
</style>