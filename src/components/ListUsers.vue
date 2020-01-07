<template>
  <div class="box container">
    <div class="card-list" v-for="user in users" :key="user.id" @click="showDetail(user.id)">
      {{ user.name }}
    </div>
  </div>
</template>

<script>
export default {
  name: 'List',
  props: {
    users: {
      type: Array
    }
  },
  methods: {
    showDetail (e) {
      this.$router.push(`/about/${e}`)
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
  display: flex;
  flex-direction: column;
  justify-content: center;
  border: 1px solid #173f5f;
  background-image: url('../assets/logo.png');
  background-repeat: no-repeat;
  background-position-x: 135%;
  background-position-y: 320%;
  background-size: 100px;
  width: 200px;
  height: 100px;
  margin: 8px;
  padding: 8px;
  color: #173f5f;
  cursor: pointer;
}
.card-list:hover {
  background: seagreen;
  color: #fff;
}
</style>