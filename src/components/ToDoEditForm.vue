<template>
  <!-- Main modal -->
  <div id="editModal" class="edit-modal" tabindex="-1" aria-hidden="true">
    <!-- Modal content -->
    <div class="modal-content">
      <!-- Modal body -->
      <form @submit.prevent="onSubmit" class="modal-body">
        <div class="edit-input">
          <label :id="id">Edit ToDo</label>
          <input
            type="text"
            :id="id"
            autocomplete="off"
            v-model.lazy.trim="newTodo"
            placeholder="Edit ToDo"
          />
        </div>

        <div class="btn-group">
          <button class="btn save-btn" type="submit">
            <svg
              xmlns="http://www.w3.org/2000/svg"
              width="19"
              height="18"
              viewBox="0 0 19 18"
              fill="none"
            >
              <path
                d="M15.09 0.59C14.71 0.21 14.2 0 13.67 0H2.5C1.96957 0 1.46086 0.210714 1.08579 0.585786C0.710714 0.960859 0.5 1.46957 0.5 2V16C0.5 17.1 1.4 18 2.5 18H16.5C17.6 18 18.5 17.1 18.5 16V4.83C18.5 4.3 18.29 3.79 17.91 3.42L15.09 0.59ZM9.5 16C7.84 16 6.5 14.66 6.5 13C6.5 11.34 7.84 10 9.5 10C11.16 10 12.5 11.34 12.5 13C12.5 14.66 11.16 16 9.5 16ZM10.5 6H4.5C3.4 6 2.5 5.1 2.5 4C2.5 2.9 3.4 2 4.5 2H10.5C11.6 2 12.5 2.9 12.5 4C12.5 5.1 11.6 6 10.5 6Z"
                fill="white"
              ></path>
            </svg>
            <span>Save</span>
          </button>
          <button @click="onCancel" class="btn">Cancel</button>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ToDoEditForm',
  emits: ['item-edited', 'item-cancelled'],
  props: {
    todo: {
      type: String,
      required: true
    },
    id: {
      type: String,
      required: true
    }
  },
  data() {
    return {
      newTodo: this.todo
    }
  },
  methods: {
    onSubmit() {
      if (this.newTodo && this.newTodo !== this.todo) {
        this.$emit('item-edited', this.newTodo)
      }
    },
    onCancel() {
      this.newTodo = this.todo
      this.$emit('edit-cancelled')
    }
  }
}
</script>

<style>
.edit-modal {
  margin: 2rem auto;
  background: #fff;
  box-shadow: 0px 4px 25px 0px rgba(0, 0, 0, 0.1);
  width: 100%;
  max-width: 650px;
  border-radius: 1rem;
}

.modal-content {
  display: flex;
  flex-direction: column;
  justify-content: center;
  gap: 0.5rem;
  padding: 1rem;
}

.modal-body {
  display: flex;
  flex-direction: column;
  gap: 2rem;
}

.edit-input {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.edit-input > label {
  align-self: center;
}

.edit-input > input {
  padding: 0.7rem 1rem;
  border: 1px solid #ddd;
  border-radius: 5px;
  font-size: 0.9em;
}

.save-btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 0.3rem;
}
</style>
