<template>
  <main>
    <!--heading-->
    <header>
      <img src="./assets/pinia-logo.svg" alt="pinia logo" />
      <h1>Pinia tasks</h1>
    </header>

    <!-- new task form -->
    <div class="new-task-form">
      <TaskForm />
    </div>

    <!-- filter -->
    <nav class="filter">
      <button @click="filter = 'all'">All tasks</button>
      <button @click="filter = 'favs'">Favorite tasks</button>
    </nav>

    <!-- loading -->
    <div class="loading" v-if="taskStore.loading">Loading tasks...</div>

    <!--task list-->
    <div class="task-list" v-if="filter === 'all'">
      <p>
        You have {{ taskStore.totalCount }}
        {{ taskStore.totalCount === 1 ? "task" : "tasks" }} left to do.
      </p>
      <div v-for="task in taskStore.tasks" :key="task.id">
        <TaskDetails :task="task" />
      </div>
    </div>
    <div class="task-list" v-if="filter === 'favs'">
      <p>You have {{ taskStore.favCount }} tasks in your favorite list.</p>
      <div v-for="task in taskStore.favs" :key="task.id">
        <TaskDetails :task="task" />
      </div>
    </div>
  </main>
</template>

<script>
import { ref } from "vue";
import TaskDetails from "./components/TaskDetails.vue";
import TaskForm from "./components/TaskForm.vue";
import { useTaskStore } from "./stores/TaskStore";

export default {
  components: { TaskDetails, TaskForm },
  setup() {
    const taskStore = useTaskStore();

    // fetch tasks
    taskStore.getTasks();

    const filter = ref("all");

    return { taskStore, filter };
  },
};
</script>
