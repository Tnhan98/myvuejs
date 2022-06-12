<template>
    <AddTodo @add-item="handleAdd"/>
    <br>
    <TodoItems v-for="todo in todos" :key="todo.id" :TodoProp = "todo" @item-id = "checkCompleted" @delete-item="handleClick" />
</template>

<script>
import { ref } from 'vue'
import axios from 'axios'
import TodoItems from './TodoItems.vue'
import AddTodo from './AddTodo.vue'
export default {
    name: 'TodoList',
    components: { TodoItems, AddTodo },
    setup() {
        const todos = ref([])
        const getAllTodos = async () => {
            try {
                const res = await axios.get(`https://jsonplaceholder.typicode.com/todos?_limit=3`)
                todos.value = res.data
            } catch (error) {
                console.log(error);
            }
        }
        getAllTodos()


        const checkCompleted = (id) => {
           todos.value = todos.value.map(todo => {
                if(todo.id === id) {
                    todo.completed = !todo.completed
                }
                return todo
            })
        }
        const handleClick = async (id) => {
           try {
                await axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
                todos.value = todos.value.filter(todo => todo.id != id)
           } catch (error) {
                console.log(error);
           }
        }
        const handleAdd = async (newJob) => {
            try {
                const res = await axios.post('https://jsonplaceholder.typicode.com/todos', newJob)
                todos.value.push(res.data)

                console.log(todos);
            } catch (error) {
                console.log(error);
            }
        }
       
        return {
            todos,
            checkCompleted,
            handleClick,
            handleAdd,
            getAllTodos
        }
    }
}
</script>

<style>

</style>