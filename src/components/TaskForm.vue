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
  //   setup() {
  //     const taskStore = useTaskStore();

  //     const newTask = ref("");

  //     const handleSubmit = () => {
  //       if (newTask.value.length > 0) {
  //         taskStore.addTask({
  //           title: newTask.value,
  //           isFav: false,
  //           id: Math.floor(Math.random() * 1000000),
  //         });
  //         newTask.value = "";
  //       }
  //     };

  //     return { handleSubmit, newTask };
  //   },
  data() {
    return {
      taskStore: useTaskStore(),
      newTask: ref(""),
    };
  },
  methods: {
    handleSubmit() {
      if (this.newTask.length > 0) {
        this.taskStore.addTask({
          title: this.newTask,
          isFav: false,
          id: Math.floor(Math.random() * 1000000),
        });
        this.newTask = "";
      }
    },
  },
};
</script>
