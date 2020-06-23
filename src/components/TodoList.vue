<template>
    <div class="container">
        <div class="row">
            <div class="col-12">
                <p class="display-3">Vue Crash Course</p>
            </div>
        </div>
        <div class="row">
            <p>Add Create Form</p>
        </div>
        <div class="row">
            <div class="col-12 col-lg-6">
                <ul class="list-group">
                    <Todo v-for="(todo, index) in todos" :key="index"
                        :todoString="todo.todoString"
                        :completed="todo.completed"
                     />
                </ul>
            </div>
        </div>
    </div>
</template>

<script>
import Todo from "./todo";
export default {
    components:{
        Todo
    },
    data(){
        return{
            todos:[
                {todoString: "Wake Early", completed:true},
                {todoString: "Learn Cooking", completed:false},
                {todoString: "Do Competitive Coding", completed:true},
                {todoString: "Start Investment", completed:false},
                {todoString: "Eat Healthy", completed:false},
                {todoString: "Complete GoLang", completed:true}
            ]
        };
    },
    methods:{
        addTodo(newTodo){
            this.todos.push({
                todoString: newTodo,
                completed:false
            });
        },
        toggleTodo(todo){
            todo.completed=!todo.completed;
        },
        editTodo(todo,newTodoString){
            todo.todoString=newTodoString;
        },
        deleteTodo(deleteTodo){
            this.todos=this.todos.filter(todo => todo.todoString !== deleteTodo.todoString);
        }
    }
}
</script>

<style>

</style>