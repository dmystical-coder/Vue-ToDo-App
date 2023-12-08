<template>
  <form @submit.prevent="onSubmit">
    <div class="input-group">
      <div class="input">
        <input
          @focus="resetStyles"
          :style="style2"
          type="text"
          name="new-todo"
          v-model.lazy.trim="todoContent"
          id="new-todo-input"
          autocomplete="off"
          placeholder="What needs to be done?"
        />
        <label for="new-todo-input" :style="style">You have to enter some text!</label>
      </div>
      <button class="btn" type="submit">Add ToDo</button>
    </div>
  </form>
</template>

<script>
export default {
  data() {
    return {
      style: {
        display: 'none',
        fontSize: '0.875rem',
        fontWeight: '500',
        color: '#f31623'
      },
      style2: {
        borderColor: ''
      },
      todoContent: ''
    }
  },
  methods: {
    onSubmit() {
      if (this.todoContent === '') {
        this.style.display = 'block'
        this.style2.borderColor = '#f31623'
        return
      }
      this.$emit('todo-added', this.todoContent)
      this.todoContent = ''
    },
    resetStyles() {
      this.style.display = 'none'
      this.style2.borderColor = ''
    }
  }
}
</script>

<style scoped>
.input {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}
</style>
