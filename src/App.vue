<template>
  <div class="card">
    <h1>To-Do App</h1>
    <to-do-form @todo-added="addToDo"></to-do-form>

    <div class="todos-list">
      <h2>
        <svg
          xmlns="http://www.w3.org/2000/svg"
          width="24"
          height="24"
          viewBox="0 0 18 20"
          fill="none"
        >
          <path
            d="M15 8L13.59 6.58L7 13.17L4.41 10.59L3 12L7 16L15 8ZM16 2H11.82C11.4 0.84 10.3 0 9 0C7.7 0 6.6 0.84 6.18 2H2C1.86 2 1.73 2.01 1.6 2.04C1.21 2.12 0.86 2.32 0.59 2.59C0.41 2.77 0.26 2.99 0.16 3.23C0.0600001 3.46 0 3.72 0 4V18C0 18.27 0.0600001 18.54 0.16 18.78C0.26 19.02 0.41 19.23 0.59 19.42C0.86 19.69 1.21 19.89 1.6 19.97C1.73 19.99 1.86 20 2 20H16C17.1 20 18 19.1 18 18V4C18 2.9 17.1 2 16 2ZM9 1.75C9.41 1.75 9.75 2.09 9.75 2.5C9.75 2.91 9.41 3.25 9 3.25C8.59 3.25 8.25 2.91 8.25 2.5C8.25 2.09 8.59 1.75 9 1.75ZM16 18H2V4H16V18Z"
            fill="#323232"
          />
        </svg>
        <span>To-Dos</span>
      </h2>
      <ul>
        <li v-for="item in todos" :key="item.id">
          <to-do-item
            :todo="item.todo"
            :id="item.id"
            :completed="item.completed"
            @checkbox-changed="updateCompletedStatus(item.id)"
            @item-changed="updateTodoContent(item.id, $event)"
            @item-deleted="deleteTodo(item.id)"
          ></to-do-item>
        </li>
      </ul>
    </div>
    <to-do-footer @clear-all="clearAllTodos" @clear-completed="clearCompletedTodos" :listSummary="listSummary"></to-do-footer>
  </div>
</template>

<script>
import uniqueid from 'lodash/uniqueId'
import ToDoForm from '@/components/ToDoForm.vue'
import ToDoItem from '@/components/TodoItem.vue'
import ToDoFooter from '@/components/TodoFooter.vue'

export default {
  name: 'App',
  components: {
    ToDoForm,
    ToDoItem,
    ToDoFooter
  },
  data() {
    return {
      todos: [
        {
          id: uniqueid('todo-'),
          todo: 'Do something nice for someone I care about',
          completed: true,
          userId: 26
        },
        {
          id: uniqueid('todo-'),
          todo: 'Memorize the fifty states and their capitals',
          completed: false,
          userId: 48
        },
        {
          id: uniqueid('todo-'),
          todo: 'Watch a classic movie',
          completed: true,
          userId: 4
        }
      ]
    }
  },
  methods: {
    addToDo(todoContent) {
      this.todos.push({
        id: uniqueid('todo-'),
        todo: todoContent,
        completed: false
      })
    },
    updateCompletedStatus(todoId) {
      const todoToUpdate = this.todos.find((item) => item.id === todoId);
      todoToUpdate.completed = !todoToUpdate.completed
    },
    updateTodoContent(todoId, newTodo){
      const todoToUpdate = this.todos.find((item) => item.id === todoId);
      todoToUpdate.todo = newTodo;
    },
    deleteTodo(todoId){
      const todoIndex = this.todos.findIndex((item) => item.id === todoId);
      this.todos.splice(todoIndex, 1);
    },
    clearAllTodos(){
      this.todos = [];
    },
    clearCompletedTodos(){
      const uncompletedTodos = this.todos.filter((item) => item.completed === false);
      this.todos = uncompletedTodos;
    }
  },
  computed: {
    listSummary() {
      const numberOfFinishedItems = this.todos.filter((item) => item.completed).length
      return `${numberOfFinishedItems} out of ${this.todos.length} items completed`
    }
  }
}
</script>

<style scoped>
.todos-list {
  padding: 0 1.2rem;
  width: 100%;
}
h2 {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.5rem;
  font-size: 1.5rem;
}
li {
  font-size: 1rem;
  font-weight: 400;
  padding: 1.1rem 0;
  border-bottom: 2px solid #d0d0d0;
}

@media screen and (min-width: 620px) {
  h2 {
    justify-content: flex-start;
  }
  li {
    font-size: 1.25rem;
  }
}
</style>
