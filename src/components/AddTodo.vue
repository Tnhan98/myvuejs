<template>
    <form class="form">
        <input class="input" placeholder="Enter your job..." v-model="job">
        <button class="add-btn" @click="handleAdd">Add</button>
    </form>
</template>

<script>
import { ref } from 'vue'
export default {
    name: 'add-todo',
    setup(props, context) {
        const job =ref('')
        const handleAdd = (event) => {
            event.preventDefault()
            const newJob = {
                title: job.value,
                completed: false
            }
        context.emit('add-item', newJob)
        job.value = ''
        job.value = focus()
        }
        return {
            job,
            handleAdd,
        }
    }
       
   
}
</script>

<style lang="scss">
.form {
    display: flex;
    justify-content: center;
    margin: 10px;
    padding: 15px;
}
.input {
    border-radius: 15px;
    padding: 5px;
    margin: 5px;
    height: 40px;
    min-width: 300px;
    background-color: #ccc;
    line-height: 1.5;
    cursor: pointer;
    border: 1px #333 solid;
    &:hover {
        border: 1px #ccc solid;
    }
}
.add-btn {
    padding: 10px;
    margin: 5px;
    min-width: 100px;
    cursor: pointer;
    border-radius: 10px;
    border: none;
    &:hover {
        background-color: #ccc;
    }
}
</style>