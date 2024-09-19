<template>
  <main>
    <!--heading-->
    <header>
      <img src="./assets/pinia-logo.svg" alt="pinia logo" />
      <h1>Pinia tasks</h1>
    </header>

    <!--task list-->
    <div class="task-list">
      <div v-for="task in taskStore.tasks" :key="task.id">
        {{ task.title }}
      </div>
    </div>
  </main>
</template>

<script>
import { useTaskStore } from "./stores/TaskStore";
export default {
  setup() {
    const taskStore = useTaskStore();

    return { taskStore };
  },
};
</script>
