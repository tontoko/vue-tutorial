<template>
  <div>
    {{ msg }}
    <form>
      <button @click="addTodo()">ADD TASK</button>
      <button @click="removeTodo()">DELETE FINISHED TASKS</button>
      <p>input: <input type="text" v-model="newTodo"></p>
      <p>task: {{newTodo}}</p>
    </form>
    <div class="task-list">
      <label class="task-list__item"
             v-for="todo in todos"
             :key="todo.i"
             v-bind:class="{'task-list__item--checked': todo.done}">
        <input type="checkbox" v-model="todo.done">
        <input type="checkbox" v-model="todo.editing">
        <input v-if="todo.editing" v-model="todo.text" @keyup.enter="todo.editing = !todo.editing">
        <button>EDIT</button>
        {{todo.text}}
      </label>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      todos: [
        {text: 'vue-router', done: false, editing: false, i: 1},
        {text: 'vuex', done: false, editing: false, i: 2},
        {text: 'vue-loader', done: false, editing: false, i: 3},
        {text: 'awesome-vue', done: true, editing: false, i: 4}
      ],
      newTodo: '',
      i: 4
    }
  },
  methods: {
    addTodo: function (evnet) {
      let text = this.newTodo && this.newTodo.trim()
      if (!text) return
      this.i++
      this.todos.push({
        text,
        done: false,
        editing: false,
        key: this.i
      })
      this.newTodo = ''
    },
    removeTodo: function (event) {
      this.todos = [...this.todos].filter(v => !v.done)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
@mixin flex-vender() {
  display: flex;
  display: -webkit-flex;
  display: -moz-flex;
  display: -ms-flex;
  display: -o-flex;
}
.task-list {
  @include flex-vender;
  flex-direction: column;
  align-items: center;
  &__item {
    width: 270px;
    text-align: left;
    $element: #{&};
    &--checked {
      @extend #{$element};
      color: #85a6c6;
    }
  }
}
</style>
