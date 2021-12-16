<template>
  <div>
    <AddTodo @add-todo="addTodo" :todoProps="todos" />
    <TodoItem
      v-for="todo in todos"
      :key="todo.id"
      :todoProps="todo"
      @item-completed="markCompleted"
      @delete-item="deleteTodo"
    />
  </div>
</template>

<script>
import { ref } from 'vue'

import TodoItem from './TodoItem.vue'
import AddTodo from './AddTodo.vue'
import axios from 'axios'
//import { v4 as uuidv4 } from 'uuid'
console.log(TodoItem)
export default {
  name: 'Todos',
  components: { TodoItem, AddTodo },
  setup() {
    const todos = ref([])
    const getAllTodos = async () => {
      try {
        const res = await axios.get(
          'https://jsonplaceholder.typicode.com/todos?_limit=10'
        )
        console.log(res.data)
        todos.value = res.data
      } catch (error) {
        console.log(error)
      }
    }
    getAllTodos()

    const markCompleted = id => {
      console.log(id)
      todos.value = todos.value.map(todo => {
        if (todo.id == id) {
          todo.isCompleted = !todo.isCompleted
        }
        return todo
      })
    }

    const deleteTodo = async id => {
      try {
        await axios.delete('https://jsonplaceholder.typicode.com/todos/' + id)
        todos.value = todos.value.filter(todo => {
          return todo.id != id
        })
      } catch (error) {
        console.log(error)
      }
    }

    const addTodo = async newItem => {
      const res = await axios.post(
        'https://jsonplaceholder.typicode.com/todos',
        newItem
      )
      todos.value.push(res.data)
    }
    return { todos, markCompleted, deleteTodo, addTodo, getAllTodos }
  }
}
</script>

<style></style>
