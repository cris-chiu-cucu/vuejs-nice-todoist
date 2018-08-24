<template>
  <div id="app" class="main-container">
    <todo-list></todo-list>
  </div>
</template>

<script>
import TodoList from './components/TodoList.vue';

export default {
  components: { TodoList }
};
</script>

<style scoped>
.main-container {
  background-image: url('./assets/images/todoist-background.jpg');
  background-size: cover;
  display: flex;
  min-height: 100vh;
  justify-content: center;
  align-items: center;
  overflow: auto;
}
</style>
