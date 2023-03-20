<script setup>
import { ref } from 'vue';
import { uid } from 'uid';
import TodoCreator from '../components/TodoCreator.vue';
import TodoItem from '../components/TodoItem.vue';
import { Icon } from '@iconify/vue';

const todoList = ref([]);

const fetchTodoList = () => {
  const todoListFromLocalStorage = JSON.parse(localStorage.getItem('todoList'));
  if (todoListFromLocalStorage) {
    todoList.value = todoListFromLocalStorage;
  }
};

fetchTodoList();

const setTodoListLocalStorage = () => {
  localStorage.setItem('todoList', JSON.stringify(todoList.value));
};

const createTodo = (todo) => {
  todoList.value.push({
    id: uid(),
    todo,
    isCompleted: null,
    isEditing: null,
  });
  setTodoListLocalStorage();
};

const toggleEditTodo = (index) => {
  todoList.value[index].isEditing = !todoList.value[index].isEditing;
  setTodoListLocalStorage();
};

const toggleTodoComplete = (index) => {
  todoList.value[index].isCompleted = !todoList.value[index].isCompleted;
  setTodoListLocalStorage();
};

const updateTodo = (todo, index) => {
  todoList.value[index].todo = todo;
  setTodoListLocalStorage();
};
</script>

<template>
  <main>
    <h1>Create Todo</h1>
    <TodoCreator @create-todo="createTodo" />
    <ul>
      <TodoItem
        v-for="(todo, index) in todoList"
        :todo="todo"
        :index="index"
        @toggle-complete="toggleTodoComplete"
        @edit-todo="toggleEditTodo"
        @update-todo="updateTodo"
        @delete-todo="todoList.splice(index, 1)"
      />
    </ul>
    <p class="todos-message" v-if="todoList.length === 0">
      <Icon icon="noto-v1:sad-but-relieved-face" />
      <span>You have no todos to complete. Add one!</span>
    </p>
  </main>
</template>

<style lang="scss" scoped>
main {
  display: flex;
  flex-direction: column;
  max-width: 500px;
  width: 100%;
  margin: 0 auto;
  padding: 40px 16px;

  h1 {
    margin-bottom: 16px;
    text-align: center;
  }

  .todos-message {
    display: flex;
    align-items: center;
    justify-content: center;
    margin-top: 16px;
    opacity: 0.5;
    transition: 250ms ease;

    span {
      margin-left: 8px;
    }
  }
}
</style>
