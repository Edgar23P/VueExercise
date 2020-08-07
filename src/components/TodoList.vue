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
                {todoString:'code landing page',completed:false},
                {todoString:'code some stuff in backend',completed:false},
                {todoString:'meeting with Recommend',completed:true},
                {todoString:'meeting with the Cars App',completed:false}
            ]
        }
    },
    methods:{
        fetchData(){
           fetch('https://jsonplaceholder.typicode.com/todos/')
            .then(response => response.json())
            .then(json => console.log(json))
        },
        addTodo(newTodo){
            this.todos.push({
                todoString:newTodo,
                completed:false
            })
        },
        toggleTodo(todo){
            todo.completed = !todo.completed;
        },
        editTodo(todo,newTodoString){
            todo.todoString =  newTodoString;
        },
        deleteTodo(deleteTodo){
            this.todos =  this.todos.filter(todo => todo !== deleteTodo);
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