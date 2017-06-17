<template>
  <div class="todo">

    <h1>{{ msg }}</h1>
    <el-form :inline="true" class="todo-input-inline">
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

    <div class="footer" v-show="todos.length">
      <span class="todo-count">
        <strong>{{ remaining }}</strong> {{ remaining | pluralize }} left
      </span>
    </div>

  </div>
</template>

<script>
var filters = {
  all: function (todos) {
    return todos
  },
  active (todos) {
    return todos.filter(function (todo) {
      return !todo.completed
    })
  },
  completed: function (todos) {
    return todos.filter(function (todo) {
      return todo.completed
    })
  }
}
export default {
  name: 'todo',
  data () {
    return {
      msg: 'Todo App',
      newtodo: '',
      todos: []
    }
  },
  filters: {
    pluralize (n) {
      return n === 1 ? 'item' : 'items'
    }
  },
  methods: {
    addTodo (event) {
      event.preventDefault()
      if (this.newtodo === '') return
      this.todos.push({
        done: false,
        item: this.newtodo
      })
      this.newtodo = ''
    },
    deleteTodo (todo) {
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
  },
  computed: {
    remaining () {
      return filters.active(this.todos).length
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.todo-input-inline {
  border: 1px solid silver;
  padding: 10px
}
.el-form-item {
  margin-bottom: 0;
}
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

#todos {
  list-style: none;
  padding-left: 25px;
}

.footer {
  border: 1px solid silver;
  padding: 10px;
}
</style>
