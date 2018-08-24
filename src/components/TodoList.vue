<template>
  <div class="todo-list">
    <header class="todo-list__header">
      <span class="title">TODO Tasks</span>
      <div class="actions">
        <form class="actions__form">
          <input type="text" @input="hasError = false" id="new-task" v-model.trim="task" placeholder="What do you want to get done?" required class="form-control" :class="{'form-control--invalid': hasError}" autofocus>
          <span v-if="hasError" class="form-error-msg">Please enter a task</span>
        </form>
        <button type="button" class="btn actions__btn" title="Add a new task" @click="addItem">
          <img src="../assets/images/icons/add.svg" alt="Add new task icon">
        </button>
      </div>
    </header>
    <div class="todo-list__tasks">
      <template v-if="items.length">
        <todo-item v-for="(item, index) in items" :key="item.id" :task="item" @deleteTask="deleteTask(index)"></todo-item>
      </template>
      <template v-else>It's the moment to relax...</template>
    </div>
  </div>
</template>

<script>
import TodoItem from './TodoItem.vue';
import { Task } from '../models/task';

export default {
  data() {
    return {
      task: '',
      hasError: false,
      items: []
    };
  },

  methods: {
    addItem() {
      if (!this.task) {
        this.hasError = true;

        return;
      }

      const uuid = Date.now();
      const newTask = new Task(uuid, this.task);
      this.hasError = false;
      this.items.push(newTask);
      this.task = '';
    },

    deleteTask(index) {
      this.items.splice(index, 1);
    }
  },

  components: { TodoItem }
};
</script>


<style scoped>
.todo-list {
  background-color: #fff;
  border-radius: 10px;
  max-width: 60vw;
  min-width: 300px;
  max-height: 80vh;
  margin: 10px;
  flex-grow: 1;
  overflow: hidden;
  display: flex;
  flex-direction: column;
}

@media screen and (max-width: 300px) {
  .todo-list {
    max-width: 100%;
  }
}

.todo-list__header {
  padding: 7px 10px;
  background-color: lightseagreen;
  display: flex;
  flex-direction: column;
  flex-shrink: 0;
}

.title {
  font-size: 25px;
  font-weight: 700;
  flex-shrink: 0;
  margin-right: 25px;
  text-align: center;
}

.actions {
  display: flex;
  flex-shrink: 0;
  margin-top: 7px;
}

.actions__form {
  flex-grow: 1;
  max-width: 700px;
}

.actions__btn {
  flex-shrink: 0;
  margin-left: 5px;
}

.todo-list__tasks {
  padding: 20px;
  min-height: 100px;
  overflow: auto;
  flex-grow: 1;
}

.form-error-msg {
  color: red;
}
</style>
