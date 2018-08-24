<template>
  <div class="todo-item">
    <div class="content">
      <template v-if="isEditMode">
        <form class="edit-form">
          <input type="text" v-model.trim="task.label" autofocus class="form-control">
          <button type="button" class="btn" title="Close edit mode" @click="closeEditMode" :disabled="isFormValid">
            <img src="../assets/images/icons/save.svg" alt="Save btn">
          </button>
        </form>
      </template>
      <template v-else>
        <span class="check" @click="deleteTask"></span>
        <span class="label">{{ task.label }}</span>
      </template>
    </div>
    <div class="actions" v-if="!isEditMode">
      <button type="button" class="btn" title="Edit task label" @click="editTask">
        <img src="../assets/images/icons/edit.svg" alt="Edit icon">
      </button>
      <button type="button" class="btn" title="Delete task" @click="deleteTask">
        <img class="delete-icon" src="../assets/images/icons/delete.svg" alt="Delete icon">
      </button>
    </div>
  </div>
</template>

<script>
import { Task } from '../models/task';

export default {
  props: {
    task: Task
  },

  data() {
    return {
      isEditMode: false
    };
  },

  computed: {
    isFormValid() {
      return this.task.label === '';
    }
  },

  methods: {
    editTask() {
      this.isEditMode = true;
    },

    deleteTask() {
      this.$emit('deleteTask');
    },

    closeEditMode() {
      this.isEditMode = false;
    }
  }
};
</script>

<style scoped>
.todo-item {
  background-color: antiquewhite;
  padding: 7px 10px;
  border: 1px solid grey;
  border-radius: 10px;
  margin-bottom: 10px;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  overflow: hidden;
}

.todo-item:last-child {
  margin-bottom: 0;
}

.content {
  display: flex;
  align-items: center;
  flex-grow: 1;
  overflow: hidden;
}

.check {
  display: inline-block;
  border: 1px solid lightseagreen;
  background-color: #fff;
  border-radius: 2px;
  width: 18px;
  height: 18px;
  margin-right: 15px;
  flex-shrink: 0;
}

.label {
  text-overflow: ellipsis;
  overflow: hidden;
  flex-grow: 1;
  word-wrap: break-word;
}

.edit-form {
  display: flex;
  width: 100%;
}

.actions {
  display: flex;
  flex-shrink: 0;
  justify-content: flex-end;
  padding-left: 20px;
}

.btn {
  margin-left: 5px;
}

.delete-icon {
  margin-left: 2px;
}
</style>
