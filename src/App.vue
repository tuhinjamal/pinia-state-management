<template>
  <main>
    <header>
      <img src="./assets/pinia-logo.svg" alt="pinia-logo" />
      <h1>Pinia Task</h1>
      {{ data.name }}
    </header>
    <div class="new-task-form">
      <TaskForm />
    </div>
    <nav class="filter">
      <button @click="filter = 'all'">All tasks</button>
      <button @click="filter = 'favs'">Fav tasks</button>
    </nav>
    <!-- loading -->
    <div class="loading" v-if="data.loading">Loading task...</div>
    <div class="task-list" v-if="filter === 'all'">
      <p>You have {{ data.totalCount }} tasks left to do</p>
      <div v-for="(task, index) in data.tasks" :key="index">
        <TaskDetails :task="task" />
      </div>
    </div>
    <div class="task-list" v-if="filter === 'favs'">
      <p>You have {{ data.favCount }} tasks in your favs list.</p>

      <div v-for="(task, index) in data.favs" :key="index">
        <TaskDetails :task="task" />
      </div>
    </div>
    <button @click="data.$reset">reset state</button>
  </main>
</template>
<script>
import TaskDetails from "./components/TaskDetails.vue";
import TaskForm from "./components/TaskForm.vue";
import { useTaskStore } from "./stores/TaskStore";
import { storeToRefs } from "pinia";
import { ref } from "vue";
export default {
  data() {
    return {
      data: useTaskStore(),
      filter: ref("all"),
    };
  },
  created() {
    this.data.getTasks();
  },
  components: {
    TaskDetails,
    TaskForm,
  },
  setup() {
    const taskStore = useTaskStore();

    const { tasks, loading, favs, totalCount, favCount } =
      storeToRefs(taskStore);

    // fetch tasks
    taskStore.getTasks();

    const filter = ref("all");

    return { taskStore, filter, tasks, loading, favs, totalCount, favCount };
  },
};
</script>
