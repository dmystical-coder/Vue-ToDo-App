<template>
  <div class="outer-div">
    <div class="form-group">
      <input type="checkbox" :id="id" :checked="completed" @change="updateCheckStatus" />
      <label :for="id">{{ todo }}</label>
    </div>
    <div class="action-btn-group">
      <button type="button" @click="toggleItemToEditForm">
        <img src="../assets/edit.svg" alt="" /> <span class="gray">Edit</span>
      </button>
      <button type="button" @click="triggerDelete">
        <img src="../assets/delete.svg" alt="" /> <span class="red">Delete</span>
      </button>
    </div>
  </div>

  <to-do-edit-form
    v-show="isEditing"
    :id="id"
    :todo="todo"
    @item-edited="itemEdited"
    @edit-cancelled="editCancelled"
  ></to-do-edit-form>
</template>

<script>
import ToDoEditForm from './ToDoEditForm.vue'

export default {
  components: {
    ToDoEditForm
  },
  props: {
    id: {
      required: true,
      type: String
    },
    todo: {
      required: true,
      type: String
    },
    completed: {
      default: false,
      type: Boolean
    }
  },
  data() {
    return {
      isEditing: false
    }
  },
  emits: ['checkbox-changed', 'item-changed'],
  methods: {
    updateCheckStatus(){
      this.$emit('checkbox-changed');
    },
    toggleItemToEditForm() {
      this.isEditing = true
    },
    itemEdited(newTodo){
      this.$emit('item-changed', newTodo);
      this.isEditing = false;
    },
    editCancelled() {
      this.isEditing = false
    },
    triggerDelete(){
      this.$emit('item-deleted');
    }
  }
}
</script>

<style scoped>
.outer-div {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  justify-content: center;
}

.form-group {
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

button {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 0.25rem;
  cursor: pointer;
  margin-right: 0.5rem;
  background-color: transparent;
  outline: none;
  border: none;
}

.action-btn-group {
  display: inline-flex;
  align-items: center;
  gap: 1rem;
}

.red {
  font-size: 0.875rem;
  color: #f31623;
}
.gray {
  font-size: 0.875rem;
  color: #b0b0b0;
}

@media screen and (min-width: 620px) {
  div:first-of-type {
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
  }
  .action-btn-group {
    gap: 1.5rem;
  }

  .red,
  .gray {
    font-size: 1rem;
  }
}
</style>
