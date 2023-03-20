<script setup>
import { Icon } from '@iconify/vue';
const props = defineProps({
  todo: {
    type: Object,
    required: true,
  },
  index: {
    type: Number,
    required: true,
  },
});

defineEmits(['toggle-complete', 'edit-todo', 'update-todo', 'delete-todo']);
</script>

<template>
  <li>
    <input
      type="checkbox"
      :checked="todo.isCompleted"
      @input="$emit('toggle-complete', index)"
    />
    <div class="todo">
      <input
        v-if="todo.isEditing"
        type="text"
        :value="todo.todo"
        @input="$emit('update-todo', $event.target.value, index)"
      />
      <span v-else :class="{ 'completed-todo': todo.isCompleted }">
        {{ todo.todo }}
      </span>
    </div>
    <div class="todo-actions">
      <Icon
        v-if="todo.isEditing"
        icon="ant-design:check-circle-outlined"
        @click="$emit('edit-todo', index)"
        @keydown.enter="$emit('edit-todo', index)"
        tabindex="0"
      />
      <Icon
        v-else
        icon="ant-design:edit-outlined"
        @click="$emit('edit-todo', index)"
        @keydown.enter="$emit('edit-todo', index)"
        tabindex="0"
      />
      <Icon
        icon="ant-design:delete-outlined"
        @click="$emit('delete-todo')"
        @keydown.enter="$emit('delete-todo')"
        tabindex="0"
      />
    </div>
  </li>
</template>

<style lang="scss" scoped>
li {
  list-style: none;
  margin-top: 16px;
  border: 1px solid #f5f5f5;
  background-color: #f5f5f5;
  display: flex;
  align-items: center;
  padding: 8px 16px;

  &:hover {
    .todo-actions {
      opacity: 1;
    }
  }

  input[type='checkbox'] {
    appearance: none;
    height: 24px;
    width: 24px;
    background-color: #fff;
    border-radius: 50%;
    box-shadow: 0 4px 6px -1px rgb(0 0 0 / 0.1),
      0 2px 4px -1px rgb(0 0 0 / 0.06);

    &:checked {
      background-color: #41b080;
    }
  }

  .todo {
    display: flex;
    flex: 1;
    align-items: center;
    gap: 16px;
    padding: 8px 16px;
    border: 1px solid #f5f5f5;
    border-radius: 4px;
    transition: 250ms ease;

    input[type='text'] {
      width: 100%;
      padding: 8px 16px;
      border: none;

      &:focus {
        outline: none;
      }
    }

    .completed-todo {
      text-decoration: line-through;
    }
  }

  .todo-actions {
    opacity: 0;
    display: flex;
    gap: 16px;
    padding: 8px 16px;
    border: 1px solid #f5f5f5;
    border-radius: 4px;
    transition: 250ms ease;

    button {
      padding: 8px 16px;
      border: 1px solid #ccc;
      cursor: pointer;
    }
  }
}
</style>
