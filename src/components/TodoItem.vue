<template>
  <p :class="['todo-item', todoProps.isCompleted ? 'iscompleted' : '']">
    <input
      type="checkbox"
      :checked="todoProps.isCompleted"
      @change="markItemCompleted"
    />
    {{ todoProps.title }}
    <button class="del-btn" @click="deleteItem">Delete</button>
  </p>
</template>

<script>
//import { ref } from 'vue'

export default {
  name: 'TodoItem',
  props: ['todoProps'],
  setup(props, context) {
    const markItemCompleted = () => {
      context.emit('item-completed', props.todoProps.id)
      console.log(props.todoProps)
    }

    const deleteItem = () => {
      context.emit('delete-item', props.todoProps.id)
    }

    return {
      markItemCompleted,
      deleteItem
    }
  }
}
</script>

<style>
.del-btn {
  background: red;
  color: #fff;
  border: none;
  cursor: pointer;
  float: right;
}

.todo-item {
  background: #f4f4f4;
  margin: 0;
  padding: 10px;
  border-bottom: 1px #ccc dotted;
}

.iscompleted {
  text-decoration: line-through;
}
</style>
