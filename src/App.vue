<template>
  <div id="app">
    <todo-header></todo-header>
    <todo-input v-on:addTodo="addTodo"></todo-input>
    <todo-list v-bind:propsdata="todoItems" @removeTodo="removeTodo"></todo-list>
    <todo-footer v-on:clearAllItems="clear"></todo-footer>
  </div>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue';
import TodoInput from './components/TodoInput.vue';
import TodoList from './components/TodoList.vue';
import TodoFooter from './components/TodoFooter.vue';

export default {
  data(){
    return{
      todoItems: []
    }
  },
  created(){
      if(localStorage.length >0){
          for(var i=0; i<localStorage.length; i++){
              if(localStorage.key(i) != "loglevel:webpack-dev-server")
              this.todoItems.push(localStorage.key(i));
          }
      }
  },
methods:{
     addTodo(todoItem){
       localStorage.setItem(todoItem, todoItem);
       this.todoItems.push(todoItem);
      },
      clear(){
         localStorage.clear();
         this.todoItems=[];
      },
      removeTodo(todoItem, index){
        localStorage.removeItem(todoItem);
        this.todoItems.splice(index,1);
      }
  },
  components:{
    'TodoHeader': TodoHeader,
    'TodoInput': TodoInput,
    'TodoList': TodoList,
    'TodoFooter': TodoFooter
  }

}
</script>

<style>
 body{
   text-align: center;
   background-color: #F6F6F8;
 }
 input{
   border-style: groove;
   width: 200px;
 }
 button{
   border-style: groove;
 }
 .shadow{
   box-shadow: 5px 10px 10px rgb(0, 0, 0, 0.03)
 }
</style>