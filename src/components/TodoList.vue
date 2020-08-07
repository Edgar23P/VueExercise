<template>
    <div>
       <div class="container">
           <div class="row">
               <div class="col-12"> 
                   <p class="display-3">Vue Crash course</p>
                </div>
           </div>
           <div class="row">
               <div class="col-12 col-lg-6">
                   <div v-if="loading" class="spinner-border" role="status">
                        <span class="sr-only">Loading...</span>
                    </div>
                    <div v-else></div>
               <NewTodo
               @on-addTodo="addTodo($event)"
               />
               </div>
           </div>
           <div class="row">
               <div class="col-12 col-lg-6"> 
                   <ul class="list-group">
                       <Todo v-for="(todo, index) in todos" :key="index"
                       :todoString="todo.todoString"
                       :completed="todo.completed"
                       @on-delete="deleteTodo(todo)"
                       @on-toggle="toggleTodo(todo)"
                       @on-edit="editTodo(todo,$event)"
                       @on-addtodo="addTodo($event)"
                       />
                   </ul>
                </div>
           </div>
       </div>
    </div>    
</template>

<script>
import 'bootstrap'
import 'bootstrap/dist/css/bootstrap.min.css'
import Todo from './Todo';
import NewTodo from './newTodo.vue';
export default {
    name:'TodoList',
    props:{
        msg:String
    },
    components:{
        Todo,
        NewTodo
    },
    data(){
        return{
            loading:false,
            posts:null,
            todos :[
               
            ]
        }
    },
    methods:{
        fetchData(){
           fetch('http://192.168.0.147:3000/todo/')
            .then(response => response.json())
            .then(json =>this.todos = json.map(element=>{
                let complete = element.completed === 0 ? false : true;
                return{
                    id:element.id,
                    todoString:element.todoString,
                    completed:complete
                }
            }))
            
        },
        addTodo(newTodo){
            /*this.todos.push({
                todoString:newTodo,
                completed:false
            })*/
            this.loading =  true;
            let data = {
                todoString:newTodo,
                completed:0
            }
             fetch('http://192.168.0.147:3000/todo/', {
                method: 'POST', // *GET, POST, PUT, DELETE, etc.
                mode: 'cors', // no-cors, *cors, same-origin
                cache: 'no-cache', // *default, no-cache, reload, force-cache, only-if-cached
                headers: {
                'Content-Type': 'application/json'
                },
                body: JSON.stringify(data) 
                }).then(response=>{
                    console.log(response);
                    this.fetchData();
                    this.loading= false;
                });
                
        },
        toggleTodo(todo){
            //todo.completed = !todo.completed;
            this.loading = true;
             fetch('http://192.168.0.147:3000/todo/', {
                method: 'DELETE', // *GET, POST, PUT, DELETE, etc.
                mode: 'cors', // no-cors, *cors, same-origin
                cache: 'no-cache', // *default, no-cache, reload, force-cache, only-if-cached
                headers: {
                'Content-Type': 'application/json'
                },

                }).then(response=>{
                    console.log(response);
                    this.fetchData();
                    this.loading= false;
                });
        },
        editTodo(todo,newTodoString){
            todo.todoString =  newTodoString;
        },
        deleteTodo(deleteTodo){
            //this.todos =  this.todos.filter(todo => todo !== deleteTodo);
            this.loading = true;
             fetch('http://192.168.0.147:3000/todo/'+deleteTodo.id, {
                method: 'DELETE', // *GET, POST, PUT, DELETE, etc.
                mode: 'cors', // no-cors, *cors, same-origin
                cache: 'no-cache', // *default, no-cache, reload, force-cache, only-if-cached
                headers: {
                'Content-Type': 'application/json'
                },

                }).then(response=>{
                    console.log(response);
                    this.fetchData();
                    this.loading= false;
                });
        }
    },
    /* Metodo para iniciar un componente*/
    created(){
        this.fetchData();
    },
}
</script>

<style scoped>
    body{
        align-content: center;
    }
</style>