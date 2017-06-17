<template>
  <div class="todo">

    <h1>{{ msg }}</h1>
    <el-form :inline="true" :model="formInline" class="demo-form-inline">
      <el-form-item>
        <el-input placeholder="何する？" v-model="newtodo" @keyup.enter.native="addTodo"></el-input>
      </el-form-item><el-form-item>
        <el-button type="primary" @click="addTodo">追加</el-button>
      </el-form-item>
    </el-form>

    <ul id="todos">
      <li v-for="todo in todos">
        <el-checkbox v-model="todo.done"></el-checkbox>
        <span v-bind:class="{ done: todo.done }">{{ todo.item }}</span>
        <i class="el-icon-delete todo-delete" @click="deleteTodo(todo)"></i>
      </li>
    </ul>

  </div>
</template>

<script>
export default {
  name: 'todo',
  data () {
    return {
      msg: 'Todo App',
      newtodo: '',
      todos: []
    }
  },
  methods: {
    addTodo: function (event) {
      event.preventDefault()
      if (this.newtodo === '') return
      this.todos.push({
        done: false,
        item: this.newtodo
      })
      this.newtodo = ''
    },
    deleteTodo: function (todo) {
      var index = this.todos.indexOf(todo)
      this.todos.splice(index, 1)
    },
    open () {
      const h = this.$createElement
      this.$notify({
        title: 'Title',
        message: h('i', { style: 'color: teal' }, 'This is a reminder')
      })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.todo {
  text-align: left;
}

.todo-delete {
  font-size: 8px;
  cursor: pointer;
}

.done {
  text-decoration: line-through;
}
</style>
