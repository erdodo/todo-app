<template>
  <div class="home">
    <h2>ToDo App</h2>
    <input type="text" class="my-3" v-model="todo" @keyup.enter="add()">
    <ul class="">
      <li v-for="item in todos" :key="item" class="card my-1">
        <div class="input_wrapper">
          <input type="checkbox"  v-model="item.done" @click="change(item.id)" class="switch_4">
          <svg class="is_checked" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 426.67 426.67">
            <path
              d="M153.504 366.84c-8.657 0-17.323-3.303-23.927-9.912L9.914 237.265c-13.218-13.218-13.218-34.645 0-47.863 13.218-13.218 34.645-13.218 47.863 0l95.727 95.727 215.39-215.387c13.218-13.214 34.65-13.218 47.86 0 13.22 13.218 13.22 34.65 0 47.863L177.435 356.928c-6.61 6.605-15.27 9.91-23.932 9.91z">
            </path>
          </svg>
          <svg class="is_unchecked" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 212.982 212.982">
            <path
              d="M131.804 106.49l75.936-75.935c6.99-6.99 6.99-18.323 0-25.312-6.99-6.99-18.322-6.99-25.312 0L106.49 81.18 30.555 5.242c-6.99-6.99-18.322-6.99-25.312 0-6.99 6.99-6.99 18.323 0 25.312L81.18 106.49 5.24 182.427c-6.99 6.99-6.99 18.323 0 25.312 6.99 6.99 18.322 6.99 25.312 0L106.49 131.8l75.938 75.937c6.99 6.99 18.322 6.99 25.312 0 6.99-6.99 6.99-18.323 0-25.313l-75.936-75.936z"
              fill-rule="evenodd" clip-rule="evenodd"></path>
          </svg>
        </div>
        <label style=" cursor: pointer;" @click="change(item.id)">{{item.todo}}</label>
        <button class="btn btn-danger btn-sm float-end "  @click="remove(item.id)">X</button>
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
          'id': this.length,
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
        const index = this.todos.indexOf(this.todos.find(item => item.id === id));
        this.todos[index].done = !this.todos[index].done;
        localStorage.setItem('todos', JSON.stringify(this.todos));
      },
      remove(id) {
        const index = this.todos.indexOf(this.todos.find(item => item.id === id));
        this.todos.splice(index, 1);
        for (var i = 0; i < this.todos.length; i++) {
          this.todos[i].id = i;
        }
        console.log(this.todos);
        this.length = this.length - 1;
        localStorage.setItem('todos', JSON.stringify(this.todos));
        localStorage.setItem('length', this.length);
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
    width: 90%;
    margin: 0 auto;
    justify-content: space-between;
    display: flex !important;
    flex-direction: row !important;
  }

  .checkbox {
    float: left;
    margin-right: 10px;
    border: 1px solid green;
  }




.btn-danger {
  width: 30px;
  height: 30px;
  border-radius: 10%;
  margin: auto 0;
}

  .input_wrapper {
    width: 80px;
    height: 40px;
    position: relative;
    cursor: pointer;
  }

  .input_wrapper input[type="checkbox"] {
    width: 80px;
    height: 40px;
    cursor: pointer;
    -webkit-appearance: none;
    -moz-appearance: none;
    appearance: none;
    background: #315e7f;
    border-radius: 2px;
    position: relative;
    outline: 0;
    -webkit-transition: all .2s;
    transition: all .2s;
  }

  .input_wrapper input[type="checkbox"]:after {
    position: absolute;
    content: "";
    top: 3px;
    left: 3px;
    width: 34px;
    height: 34px;
    background: #dfeaec;
    z-index: 2;
    border-radius: 2px;
    -webkit-transition: all .35s;
    transition: all .35s;
  }

  .input_wrapper svg {
    position: absolute;
    top: 50%;
    -webkit-transform-origin: 50% 50%;
    transform-origin: 50% 50%;
    fill: #fff;
    -webkit-transition: all .35s;
    transition: all .35s;
    z-index: 1;
  }

  .input_wrapper .is_checked {
    width: 18px;
    left: 18%;
    -webkit-transform: translateX(190%) translateY(-30%) scale(0);
    transform: translateX(190%) translateY(-30%) scale(0);
  }

  .input_wrapper .is_unchecked {
    width: 15px;
    right: 10%;
    -webkit-transform: translateX(0) translateY(-30%) scale(1);
    transform: translateX(0) translateY(-30%) scale(1);
  }

  /* Checked State */
  .input_wrapper input[type="checkbox"]:checked {
    background: #23da87;
  }

  .input_wrapper input[type="checkbox"]:checked:after {
    left: calc(100% - 37px);
  }

  .input_wrapper input[type="checkbox"]:checked+.is_checked {
    -webkit-transform: translateX(0) translateY(-30%) scale(1);
    transform: translateX(0) translateY(-30%) scale(1);
  }

  .input_wrapper input[type="checkbox"]:checked~.is_unchecked {
    -webkit-transform: translateX(-190%) translateY(-30%) scale(0);
    transform: translateX(-190%) translateY(-30%) scale(0);
  }
</style>