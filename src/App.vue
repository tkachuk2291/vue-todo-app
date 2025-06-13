
<script setup>
import todosOriginal from './data/todos';
import { ref } from 'vue';

const todos = ref(todosOriginal);
</script>

<template>
  <div class="todoapp">
    <h1 class="todoapp__title">todos</h1>

    <div class="todoapp__content">
      <header class="todoapp__header">
        <!-- this button should have `active` class only if all todos are completed -->
        <button
            type="button"
            class="todoapp__toggle-all active"
        />

        <!-- Add a todo on form submit -->
        <form>
          <input
              data-cy="NewTodoField"
              type="text"
              class="todoapp__new-todo"
              placeholder="What needs to be done?"
          />
        </form>
      </header>
      <section class="todoapp__main">
        <!-- This is a completed todo -->

        <div class="todo"
             v-for="(todo , i) of todos"
             :key="todo.id"
        >
            <label class="todo__status-label">
              <input
                  type="checkbox"
                  class="todo__status"
                  :checked="todo.completed"
                  @change="todo.completed = !todo.completed"
              />
            </label>
          <form v-if="false">
              <input class="todo__title-field" placeholder="Empty todo will be deleted" />
          </form>

          <template  v-else>
            <span  class="todo__title">{{todo.title}}</span>
            <!-- Remove button appears only on hover -->
            <button type="button" class="todo__remove" @click="todos.splice(i, 1)">
              ×
            </button>
          </template>

          <!-- overlay will cover the todo while it is being deleted or updated -->
          <div  class="modal overlay" >
            <div class="modal-background has-background-white-ter" />
            <div class="loader" />
          </div>
        </div>
      </section>
      <footer class="todoapp__footer">
          <span class="todo-count">
            3 items left
          </span>

        <!-- Active link should have the 'selected' class -->
        <nav class="filter">
          <a
              href="#/"
              class="filter__link selected"
          >
            All
          </a>

          <a
              href="#/active"
              class="filter__link"
          >
            Active
          </a>

          <a
              href="#/completed"
              class="filter__link"
          >
            Completed
          </a>
        </nav>

        <!-- this button should be disabled if there are no completed todos -->
        <button
            type="button"
            class="todoapp__clear-completed"
        >
          Clear completed
        </button>
      </footer>
    </div>

    <div class="notification is-danger is-light has-text-weight-normal">
      <button  type="button" class="delete" />
      <!-- show only one message at a time -->
      Unable to load todos
      <br />
      Title should not be empty
      <br />
      Unable to add a todo
      <br />
      Unable to delete a todo
      <br />
      Unable to update a todo
    </div>

  </div>

</template>
