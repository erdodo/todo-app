<template>
  <div class="home">
    <h2>ToDo App</h2>
    <input type="text" class="my-3" v-model="todo" @keyup.enter="add()">
    <ul class="">
      <li v-for="item in todos" :key="item" class="card my-1" @click="change(item.id)" style="display: flex; flex-direction: row;">
        <input type="checkbox" v-model="item.done" @click="change(item.id)" class="js-switch switchery-small">
        <label for="">{{item.todo}}</label>
      </li>
    </ul>
  </div>
</template>
<script>

export default {
  data() {
    return {
      todo:'',
      todos:localStorage.getItem('todos')?JSON.parse(localStorage.getItem('todos')):[],
      length:localStorage.getItem('length')?JSON.parse(localStorage.getItem('length')):0
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
      console.log(this.todos[id-1]);
      this.todos[id-1].done = !this.todos[id-1].done;
      localStorage.setItem('todos', JSON.stringify(this.todos));
    }
  },
};
</script>
<style>
li{
  list-style: none;
  background: #f4f4f4;
  padding: 10px;
  border-radius: 5px;
  text-align: left;
}
.checkbox{
  float: left;
  margin-right: 10px;
  border: 1px solid green;
}
</style>
