<template>
  <form @submit.prevent="handleSubmit">
    <input type="text" placeholder="I need to..." v-model="newTask" />
    <button>Add</button>
  </form>
</template>

<script>
import { ref } from "vue";
import { useTaskStore } from "../stores/TaskStore";

export default {
  setup() {
    const TaskStore = useTaskStore();

    const newTask = ref("");

    const handleSubmit = () => {
      if (newTask.value.length > 0) {
        TaskStore.addTask({
          title: newTask.value,
          isFav: false,
          id: TaskStore.totalCount + 100,
        });
        newTask.value = "";
      }
    };
    return { handleSubmit, newTask };
  },
};
</script>
