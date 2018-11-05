<template>
  <li>
    <label :class="{'completed': todo.completed}">
      <input type="checkbox" v-model="todo.completed" />
      {{ todo.task }}
      <button @click="deleteTodo(todo)">Delete</button>
    </label>
  </li>
</template>

<script>
export default {
  name: 'TodoListItem',
  props: {
    todo: {
      type: Object,
      required: true
    }
  }
}
</script>

<style scoped>
.completed {
  text-decoration: line-through;
}
</style>
