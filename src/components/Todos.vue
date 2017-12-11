<template>
    <div id="todos">
    <ul class="list-group">
        <li class="list-group-item"
            v-bind:class="{'completed' : todo.completed}"
            v-for="(todo,index) in todos">

            <router-link :to="{ name: 'todo', params: { id: todo.id }}">{{todo.title}}</router-link>

            <button class="btn btn-warning btn-xs pull-right"
                    @click="deleteTodo(index,todo)"
            >Delete
            </button>
            <button class="btn  btn-xs pull-right"
                    v-bind:class="[todo.completed ? 'btn-danger' : 'btn-success']"
                    @click="toggleCompletion(todo)"
            >{{todo.completed? 'Done' : 'Do'}}
            </button>
        </li>
    </ul>
    <todo-form :todos="todos"></todo-form>
    </div>
</template>

<script>
    import TodoForm from './TodoForm'

    export default {
        name: 'Todos',
        props: ['todos'],
        methods: {
            deleteTodo(index, todo){
                this.axios.delete('http://task.dev/api/todo/'+todo.id+'/delete').then(response=>{
                    console.log(response.data);
                });
                this.todos.splice(index, 1)
            },
            toggleCompletion(todo){
                this.axios.patch('http://task.dev/api/todo/'+todo.id+'/completed').then(response=>{
                    console.log(response.data);
                });
                todo.completed = !todo.completed
            }
        },
        components: {
            TodoForm
        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
    .completed {
        color: aquamarine;
        text-decoration: line-through;
    }
</style>
