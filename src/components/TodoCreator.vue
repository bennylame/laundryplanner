<script setup>
import { reactive, defineEmits } from 'vue';

const emit = defineEmits(['create-todo']);

const todoState = reactive({
  todo: '',
  invalid: null,
  errorMessage: '',
});

const createTodo = () => {
  if (todoState.todo === '') {
    todoState.invalid = true;
    todoState.errorMessage = 'Todo value cannot be empty';
    return;
  }

  emit('create-todo', todoState.todo);
  todoState.todo = '';
  todoState.invalid = null;
  todoState.errorMessage = '';
  return;
};
</script>

<template>
  <div class="input-wrapper" :class="{ 'input-error': todoState.invalid }">
    <input type="text" v-model="todoState.todo" />
    <button @click="createTodo()">Add</button>
  </div>
  <p v-if="todoState.invalid" class="error-message">
    {{ todoState.errorMessage }}
  </p>
</template>

<style lang="scss" scoped>
.input-wrapper {
  display: flex;
  border: 1px solid #41b080;
  gap: 16px;
  transition: 250ms ease;

  &.input-error {
    border: 1px solid red;
  }

  &:focus-within {
    box-shadow: 0 -4px 6px -1px rgba(0, 0, 0, 0.1),
      0 -2px 4px -1px rgba(0, 0, 0, 0.06);
  }

  input {
    flex: 1;
    padding: 8px 16px;
    border: none;

    &:focus {
      outline: none;
    }
  }

  button {
    padding: 8px 16px;
    border: 1px solid #ccc;
    cursor: pointer;
  }
}

.error-message {
  color: red;
  font-size: 12px;
  margin-top: 8px;
  text-align: center;
}
</style>
