<template>
    <form @submit.prevent="addTodo(newTodo)">
        <div class="from-group">
            <input type="text"
                   v-model="newTodo.title"
                   class="form-control"
                   placeholder="Add a new todo">
        </div>
        <br>
        <div class="form-group">
            <button class="btn btn-success" type="submit">Add Todos</button>
        </div>
    </form>
</template>

<script>
    export default {
        name: 'todo-form',
        props: ['todos'],
        data(){
            return {
                newTodo: {id: null, title: '', completed: false}
            }
        },
        methods: {
            addTodo(newTodo){
                this.axios.post('http://task.dev/api/todo/create', {'title':this.newTodo.title}).then(response=>{
                    console.log(response.data);
                })
                this.todos.push(newTodo),
                    this.newTodo = {id: null, title: '', completed: false}
            }
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
