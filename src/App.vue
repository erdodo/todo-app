<template>
  <div class="home">
    <h2>ToDo App</h2>
    <input type="text" class="my-3" v-model="todo" @keyup.enter="add()">
    <ul class="">
      <li v-for="item in todos" :key="item" class="card my-1" @click="change(item.id)"
        style="display: flex; flex-direction: row;">
        <input type="checkbox" v-model="item.done" @click="change(item.id)" class="js-switch switchery-small">
        <label for="">{{item.todo}}</label>
        <button class="btn btn-danger btn-sm float-end" @click="remove(item.id)">X</button>
      </li>
    </ul>
  </div>

</template>
<script>
  export default {
    data() {
      return {
        todo: '',
        todos: localStorage.getItem('todos') ? JSON.parse(localStorage.getItem('todos')) : [],
        length: localStorage.getItem('length') ? JSON.parse(localStorage.getItem('length')) : 0,


      };
    },
    methods: {

      add() {
        var data = {
          'id': this.length + 1,
          'todo': this.todo,
          'done': false,
        };
        this.todos[this.length] = data;
        console.log(this.todos);
        this.todo = '';
        this.length = this.length + 1;
        localStorage.setItem('todos', JSON.stringify(this.todos));
        localStorage.setItem('length', this.length);
      },
      change(id) {
        console.log(this.todos[id - 1]);
        this.todos[id - 1].done = !this.todos[id - 1].done;
        localStorage.setItem('todos', JSON.stringify(this.todos));
      },
      remove(id) {
        const index = array.indexOf(this.todos[id - 1]);
        console.log(index);
        this.todos.splice(index, 1);
        console.log(this.todos);
        localStorage.setItem('todos', JSON.stringify(this.todos));
        localStorage.setItem('length', this.length - 1);
      }
    },
  };
</script>
<style>
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    padding-top: 20px;
  }
ul {
  list-style: none;
  margin: 0;
  padding: 0;
}
  li {
    list-style: none;
    background: #f4f4f4;
    padding: 10px;
    border-radius: 5px;
    text-align: left;
    width:90%;
    margin:0 auto;
    justify-content: space-between;
  }

  .checkbox {
    float: left;
    margin-right: 10px;
    border: 1px solid green;
  }
</style>