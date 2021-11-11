<template>
    <div class="todoapp">
        <div class="main">
            <input type="checkbox" class="toggle-all" v-model="allDone"/>
             <h1>TodoList</h1>
            <input type="text" class="new-todo" placeholder="Ajouter une tache" v-model="newTodo" @keyup.enter="addTodo"/>
            <ul class="todo-list">
            <li class="todo" v-for="todo in filterdTodos" :key="todo.name" :class="{completed:todo.completed,editing:todo===editing}">
                <div class="view">
                    <input type="checkbox" v-model="todo.completed" class="toggle"/>
                   <label @dblclick="editTodo(todo)">{{todo.name}}</label>
                   <button class="destroy" @click.prevent="deleteTodo"></button>
                </div>
                <input type="text" class="edit" v-model="todo.name" @keyup="quitEdit" v-focus="editing:todo===editing">
            </li>
        </ul>
        <slot></slot>
        </div>
          <div class="footer" v-show="hasTodos">
            <h4 class="todo-count"><strong>{{remaining}} A faire</strong></h4> <br><br><br>
            <ul class="filters">
                 <li><a href="#" :class="{selected:filter==='all'}" @click.prevent="filter='all'">Toutes les taches</a></li>
                <li><a href="#" :class="{selected:filter==='todo'}" @click.prevent="filter='todo'">A faire</a></li>
                 <li><a href="#" :class="{selected:filter==='done'}" @click.prevent="filter='done'">Faites</a></li>
            </ul>
            <button v-show="completed" @click="deleteTodoCompled">Supprimer toutes taches completed</button>
        </div>
        <br>
         <br>
          <br>
           <br>
    </div>
     
</template>
<script>
import Vue from "vue";
export default {
    name:"Todos",
    data(){
        return{
            todos:[{
                name:"tache1",
                completed:true,
                }, 
               ],
            newTodo:"",
            filter:"all",
            editing:'',
        };
    },
    methods:{
        addTodo(){
           this.todos.push({
               name:this.newTodo,
               completed:false,

           })
           this.newTodo="";
        },
        deleteTodo(todo){
            this.todos=this.todos.filter(item=>item===todo);
        },
        deleteTodoCompled:()=>{
            return this.todos.filter(todo=>todo.completed);
        },
        editTodo(todo){
            this.editing=todo;
        },
        quitEdit(){
            this.editing=null;
        }
       
    },
    computed:{
        remaining(){
            return this.todos.filter(todo=>!todo.completed).length;
        },
        completed(){
            return this.todos.filter(todo=>todo.completed);
        },
        filterdTodos(){
            if(this.filter==='todo'){
                 return this.todos.filter(todo=>!todo.completed);
            }
             else if(this.filter==='done'){
                 return this.todos.filter(todo=>todo.completed);
            }
            return this.todos;
        },
        allDone:{
            get:()=>{
               return this.remaining=0;
            },
            set:(value)=>{
                if(value===true){
                    this.todos.map((todo)=>(todo.completed===value))
                }
            }
        },
        hasTodos(){
            return this.todos.length>0
        }
    },
    directives:{
        focus(element,value){
            if(value){
               Vue.nextTick(_=>{ // permet de focuser et eviter des comportements innatendus
                   element.focus();
               })
            }
        }
    }
   
};
</script>
<style lang="scss" src="./todo.scss"></style>