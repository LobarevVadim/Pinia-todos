<template>
  <main>
    <!-- heading -->
    <header>
      <img src="https://pinia.vuejs.org/logo.svg" alt="pinia logo" />
      <h1>Pinia Tasks</h1>
    </header>

    <div class="new-task-form">
      <TaskForm />
    </div>

    <nav class="filter">
      <button @click="filter = 'all'">All tasks</button>
      <button @click="filter = 'favs'">Favoite</button>
    </nav>

    <div v-if="TaskStore.loading" class="loading">Loading...</div>

    <div v-if="filter === 'all'" class="task-list">
      <p>All task( {{ TaskStore.totalCount }} )</p>
      <div v-for="task in TaskStore.tasks">
        <TaskDetails :task="task" />
      </div>
    </div>
    <div v-if="filter === 'favs'" class="task-list">
      <p>Favorite tasks( {{ TaskStore.favCounts }} )</p>
      <div v-for="task in TaskStore.favs">
        <TaskDetails :task="task" />
      </div>
    </div>
  </main>
</template>

<script>
import { ref } from "vue";
import TaskDetails from "./components/taskDetails.vue";
import TaskForm from "./components/TaskForm.vue";
import { useTaskStore } from "./stores/TaskStore";
export default {
  components: { TaskDetails, TaskForm },
  setup() {
    const TaskStore = useTaskStore();
    TaskStore.getTask();
    const filter = ref("all");
    return { TaskStore, filter };
  },
};
</script>
