<template>
  <p :class="['item-list', TodoProp.completed ? 'is-completed' : '']">
    <input type="checkbox" :checked = 'TodoProp.completed' @change="checkCompleted">
    {{ TodoProp.title }}
    <button class="delete" @click="handleClick">Deletes</button>
  </p>
</template>

<script>
// import { ref } from 'vue'
export default {
    name: 'TodoItems',
    props: ['TodoProp'],
    setup(props, context) {
      const checkCompleted = () => {
        context.emit('item-id', props.TodoProp.id)
      }
      const handleClick = () => {
        context.emit('delete-item', props.TodoProp.id)
      }
      return {
        checkCompleted,
        handleClick
        }
    }
}
</script>

<style lang="scss">
.item-list {
  background-color: #f4f4f4;
  padding: 10px 10px 15px;
  border-bottom: 1px #ccc solid;
  margin: 0;
  &:hover {
    background-color: #333;
    color: #fff
  }
}

.is-completed {
  text-decoration: line-through;
}
.delete {
  background: #ff0000;
  color: #fff;
  cursor: pointer; 
  border: none;
  float: right;
  padding: 5px;
  &:hover {
    background-color: #ccc;
    color: #333;
  }
}
</style>