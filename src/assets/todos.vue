
<template>

<section class="todoapp">
  <header class="header">
    <h1>Mon Todos</h1>
    <input type="text" class="new-todo" placeholder="ajouter une tache" v-model="newtodo" @keyup.enter="addtodo">
  </header>
  <div class="main">
    <input type="checkbox" id="toggle-all-input" class="toggle-all" v-model="alldone">
    <label class="toggle-all-label" for="toggle-all-input"> Toggle All Input </label>
    <ul class="todo-list">
      <li class="todo" v-for="todo in filtertodos"  :class="{completed:todo.completed}">
        <div class="view">
          <input type="checkbox" v-model="todo.completed" class="toggle">
          <label>{{ todo.name }}</label>
          <button class="destroy" @click.prevent="deletetodo(todo)"></button>
        </div>
      </li>
    </ul>
  </div>

  <footer class="footer">
    <span class="todo-count"><strong>{{remaining}}</strong> taches restantes</span>

    <ul class="filters" v-show="filtertodos.length >0 ">
      <li><a href="#" :class="{selected: filtre === 'all'}" @click.prevent="filtre = 'all'">toutes</a></li>
      <li><a href="#" :class="{selected: filtre === 'todo'}" @click.prevent="filtre = 'todo'">a faire</a></li>
      <li><a href="#" :class="{selected: filtre === 'donne'}" @click.prevent="filtre = 'donne'">faites</a></li>
    </ul>

    <button class="clear-completed"  @click.prevent="deletecompleted">suprime tache complete</button>
  </footer>
</section>
</template>

<script>
export default{
  data(){
    return {
      todos:[{
        name:"tache test",
        completed:false
      }],
      newtodo:'',
      filtre:'all',

    }
  },
  methods:{
    addtodo(){
      this.todos.push({
        name:this.newtodo,
        completed:false
      })
      this.newtodo=''
    },
    deletetodo(todo){
      this.todos = this.todos.filter(i=>i!=todo)
    },
    deletecompleted(){
      this.todos = this.todos.filter(todo=>!todo.completed)
    }
  },
  computed:{
    remaining(){
      return this.todos.filter(todo=>!todo.completed).length
    },
    filtertodos(){
      if(this.filtre==='todo'){
        return this.todos.filter(todo=>!todo.completed)

      } else if(this.filtre==='donne'){
        return this.todos.filter(todo=>todo.completed)

      }
      return this.todos
    },
    alldone:{
      get(){
        return this.todos.remaining=== 0
      },
      set(value){
        this.todos.forEach(todo=>todo.completed = value)
      }
    }

  },
  donetodo(){
        return this.todos.filter(todo=>todo.completed).length
  }
}
</script>

<style src ="./todos.css">

</style>
