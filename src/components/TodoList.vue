<template>
  <div>
    <button @click="todosAreFiltered = !todosAreFiltered">
      <span v-if="todosAreFiltered">Show All</span>
      <span v-else>Hide Completed</span>
    </button>

    <ul v-if="!isListEmpty">
      <todo-list-item v-for="(item, index) in displayList" :key="index" :todo="item" />
    </ul>
    <p v-else>
        Please enter a task below.
    </p>

    <div>
      <input type="text" v-model="newTask" />
      <button @click="addTask">Add</button>
      <button @click="clearTasks">Clear All Tasks</button>
    </div>

    <div>
      <input type="text" v-model="taskFilter" />
      <button @click="clearFilter">Clear Filter</button>
    </div>
  </div>
</template>

<script>
import TodoListItem from './TodoListItem'

export default {
  name: 'TodoList',
  components: {
    TodoListItem
  },

  data: () => ({
    todosAreFiltered: false,
    taskFilter: '',
    newTask: '',
    list: [
      {
        task: 'Buy milk',
        completed: true
      },
      {
        task: 'Stop at Postoffice',
        completed: false
      },
      {
        task: 'Do Express Homework',
        completed: false
      },
    ]
  }),

  computed: {
    isListEmpty () {
      return this.list.length === 0
    },
    filteredList () {
      return this.list.filter(todo => {
        return todo.task.toLowerCase().includes(this.taskFilter.toLowerCase())
      })
    },
    displayList () {
      if (this.todosAreFiltered) {
        return this.filteredList.filter((todo) => !todo.completed)
      } else {
        return this.filteredList
      }
    }
  },

  methods: {
    addTask () {
      this.list.push({
        task: this.newTask,
        completed: false
      })

      this.newTask = ''
    },
    clearTasks () {
      this.list = []
    },
    clearFilter () {
      this.taskFilter = ''
    },
    deleteTodo (todoToDelete) {
      this.list.forEach((todo, index) => {
        if (todo.task === todoToDelete.task) {
          this.list.splice(index, 1)
        }
      })
    }
  }

}
</script>

<style scoped>
ul {
  margin: 0;
  padding: 0 2em 0;
  list-style-type: none;
}
li {
  text-align: left;
}

.completed {
  text-decoration: line-through;
}
</style>
