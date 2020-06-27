<template>
    <div class="container">
        <div class="row">
            <div class="col-12">
                <p class="display-3">Vue TODO LIST</p>
            </div>
        </div>
        <div class="row">
            <div class="col-12 col-lg-6">
                <NewTodo 
                @on-addTodo ="addTodo($event)"
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
                     />
                </ul>
            </div>
        </div>
    </div>
</template>

<script>
import Todo from "./todo";
import NewTodo from './NewTodo'
export default {
    components:{
        Todo,
        NewTodo
    },
    data(){
        let localTodo=JSON.parse(localStorage.getItem('todoList'));
        console.log(localTodo);
        return{
            todos:localTodo
        };
    },
    methods:{
        addTodo(newTodo){
            this.todos.push({
                todoString: newTodo,
                completed:false
            });
            localStorage.setItem('todoList',JSON.stringify(this.todos));
        },
        toggleTodo(changeTodo){
            for(var todo in this.todos){
                if(this.todos[todo].todoString===changeTodo.todoString){
                    changeTodo.completed=!changeTodo.completed;
                }
            }
            localStorage.setItem('todoList',JSON.stringify(this.todos));
        },
        editTodo(changeTodo,newTodoString){
            for(var todo in this.todos){
                if(this.todos[todo].todoString===changeTodo.todoString){
                    changeTodo.todoString=newTodoString;
                }
            }
            localStorage.setItem('todoList',JSON.stringify(this.todos));
        },
        deleteTodo(deleteTodo){
            this.todos=this.todos.filter(todo => todo.todoString !== deleteTodo.todoString);
            localStorage.setItem('todoList',JSON.stringify(this.todos));
        }
    }
}
</script>

<style>
</style>