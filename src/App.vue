<template>
    <div id="app">
        <router-view :todos="todos"></router-view>
    </div>
</template>

<script>
    import HelloWorld from './components/HelloWorld'

    export default {
        name: 'app',
        data() {
            return {
                todos: []
            }
        },
        mounted: function () {
            this.axios.get("http://task.dev/api/todos").then(response => {
                this.todos = response.data
            console.log(response.data)
        })
        },
        computed: {
            todoCount: function () {
                return this.todos.length;
            }
        },
        components: {
            HelloWorld
        }
    }
</script>

<style>
    #app {
        font-family: 'Avenir', Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        margin-top: 60px;
    }
</style>
