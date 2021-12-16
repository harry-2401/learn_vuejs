<template>
  <form @submit="addItem">
    <input type="text" placeholder="viec moi..." v-model="title" />
    <input type="submit" value="Them" class="add-btn" />
  </form>
</template>

<script>
import { ref } from 'vue'

export default {
  name: 'AddTodo',
  props: ['todoProps'],
  setup(props, context) {
    const title = ref('')

    const addItem = event => {
      event.preventDefault()
      console.log(props.todoProps.length)
      const newItem = {
        //id: props.todoProps.length + 1,
        title: title.value,
        isCompleted: false
      }

      context.emit('add-todo', newItem)
      title.value = ''
    }

    return { title, addItem }
  }
}
</script>

<style scoped>
form {
  display: flex;
}

input[type='text'] {
  flex: 10;
  padding: 5px;
}

input[type='submit'] {
  flex: 2;
}
</style>
