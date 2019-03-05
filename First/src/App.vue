<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Home</router-link>
      <router-link to="/about">About</router-link>
      <router-view/>
      
    </div>
    <Header/>
    <AddTodo v-on:add-todo="addTodo"/>
  <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo"/>
</Todos>
    </AddTodo>
  </div>
</template>

<script>
import axios from 'axios';
import Header from './components/layouts/Header';
import Todos from './components/Todos';
import AddTodo from './components/AddTodo';

export default {
  name: 'app',
  components: {
    Header,
    Todos,
    AddTodo
  },
  data(){
    return {
      todos: [
      /*{
        id: 1,
        title: "Todo one",
        completed: false
      },{
        id: 2,
        title: "Todo two",
        completed:true
      },{
        id:3,
        title: "Todo Three",
        completed: false
      }*/

      ]      
    }

  },
  methods: {
    deleteTodo(id) {
      axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
      .then(res => this.todos = this.todos.filter(todo => todo.id !== id))
      //.catch(err => console.log(err))
      //this.todos = this.todos.filter(todo => todo.id !== id);
    },
    addTodo(newTodo) {
      const { title, completed } = newTodo;

      axios.post('https://jsonplaceholder.typicode.com/todos',{
        title,
        completed
      })
      .then( res => this.todos = [...this.todos, res.data])
      //.catch(err => console.log(err))
      //this.todos = [...this.todos, newTodo]
    }
  },
  created() {
     axios.get('https://jsonplaceholder.typicode.com/todos?_limit=10')
      .then(res => this.todos = res.data)
      //.catch(err => console.log(err));

    }
}
</script>

<style>
* {
  box-sizing: border-box;
  margin:0;
  padding:0;
}

body {
  font-family: Arial, Helvetica, sans-serif;
  line-height: 1.4;
}

.btn {
  display:inline-block;
  border:none;
  background:#555;
  color:#fff;
  padding: 7px 20px;
  cursor:pointer;
}

.btn:hover {
  background: #ccc;
}
</style>
