<template>
  <div class="todo">
    <h1>{{ msg }}</h1>
    <h2>Essential Links</h2>
    <i class="el-icon-edit"></i>
    <i class="el-icon-share"></i>
    <i class="el-icon-delete"></i>
    <el-button type="primary" icon="search">Search</el-button>
  </div>
</template>

<script>
export default {
  name: 'todo',
  data () {
    return {
      msg: 'Todo App'
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
