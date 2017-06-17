<template>
  <div class="todo">

    <el-row :gutter="20">
      <el-col :span="6" :offset="9">
        <h1>{{ msg }}</h1>

        <el-input placeholder="何する？" v-model="newtodo"></el-input>
        <el-button @click="addTodo">追加</el-button>

        <ul id="todos">
          <li v-for="todo in todos">
            {{ todo.item }}
            <i class="el-icon-delete todo-delete" @click="deleteTodo(todo)"></i>
          </li>
        </ul>
      </el-col>
    </el-row>
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
</style>
