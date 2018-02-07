<template>
  <div>
    <div class="todo-list">
      <form action="">
        <input type="text" v-model="todoList.searchQuery">
        <button type="submit" v-on:click.prevent="submitForm">Add</button>
      </form>

      <transition name="fade">
        <div v-if="todoList.searchQueryInCorrect" style="padding: 7px 0 0 10px;">
          Type more than 10 letters to Submit
        </div>
      </transition>

      <ul class="task-list">
        <li v-for="(task, index) in todoList.todoItems.tasks" v-bind:key="index" v-bind:class="{ completed : task.completed}">
          <div class="task-text">{{task.text}}</div>
          <div class="control-buttons">
            <span class="red" v-on:click.prevent="deleteItem(index)">D</span>
            <span class="green" v-on:click.prevent="completeItem(index)">C</span>
          </div>
        </li>
      </ul>

      <div class="help-info">
        <span>* <span class="red">D</span> - delete item</span>
        <span>* <span class="green">C</span> - complete item</span>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'Home',
  data () {
    return {
      header: 'VUEjs extencion',
      todoList: {
        searchQuery: '',
        searchQueryInCorrect: false,
        todoItems: {
          tasks: [
            {
              completed: false,
              text: 'Pay bills'
            },
            {
              completed: false,
              text: 'Meet George'
            },
            {
              completed: false,
              text: 'Buy Eggs'
            },
            {
              completed: false,
              text: 'Read a book'
            },
            {
              completed: false,
              text: 'Organize workflow'
            }
          ]
        }
      }
    }
  },
  computed: {
  },
  methods: {
    toUpper () {
      this.header = this.header.toUpperCase()
    },
    submitForm () {
      let todoList = this.todoList

      if (todoList.searchQuery && todoList.searchQuery.length >= 10) {
        todoList.todoItems.tasks.push({
          completed: false,
          text: todoList.searchQuery
        })
        todoList.searchQueryInCorrect = false
        todoList.searchQuery = ''
      } else if (this.searchQuery.length < 10) {
        todoList.searchQueryInCorrect = true
      }
    },
    deleteItem (index) {
      let todoList = this.todoList

      todoList.todoItems.tasks.splice(index, 1)
    },
    completeItem (index) {
      let todoList = this.todoList

      todoList.todoItems.tasks[index].completed = !todoList.todoItems.tasks[index].completed
    }
  },
  created () {
    this.toUpper()
  }
}

</script>
