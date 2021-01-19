<template>
  <div id="app">
  <Header />
  <AddTodo v-on:add-todo="addTodo"/>
  <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" />
  </div>
</template>

<script>
import Header from './components/layout/Header';
import Todos from './components/Todos';
import AddTodo from './components/AddTodo';
import axios from 'axios';

export default {
  name: 'App',
  components: {
    Header,
    Todos,
    AddTodo

  },
  data()
  {
    return {
    todos: []
    }
  },
  methods: {
    deleteTodo(id)
    {
      axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
      .then(this.todos = this.todos.filter(todo => todo.id!==id))
       .catch(err=> console.log(err));
    },
    addTodo(newTodo)
  { 
    if(newTodo.title!=''){
    const { title, completed }  = newTodo;
    axios.post('https://jsonplaceholder.typicode.com/todos',{
      title,
      completed
    })
  .then(res => this.todos = [...this.todos,res.data])
   .catch(err=> console.log(err));
    }
    else{
      alert('Please Enter Item');
    }
  }
  },
  created()
  {
    axios
    .get('https://jsonplaceholder.typicode.com/todos?_limit=5')
    .then(res => this.todos = res.data)
    .catch(err => console.log(err));
  }

}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  width: 50%;
  margin: 0 auto;
}
</style>
