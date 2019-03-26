<template>
  <div>
    <task-form @addTask="addTask"></task-form>
    <div class="container">
      <task-row
        v-for="(task, index) in tasks"
        :item="task"
        :index="index"
        :key="task.id"
        @removeTask="removeTask"
      />
    </div>
  </div>
</template>
<script>
import TaskRow from "./TaskRow";
import TaskForm from "./TaskForm";
export default {
  components: {
    TaskRow,
    TaskForm
  },
  data() {
    return {
      taskTitle: "",
      tasks: [],
      titleError: false
    };
  },
  created() {
    const tasks = JSON.parse(localStorage.getItem("tasks"));
    if (tasks) {
      this.tasks = tasks;
    }
  },
  methods: {
    idGenerator() {
      return (Date.now() - Math.random() * 16).toString(16);
    },
    addTask(title) {
      this.tasks.push({
        title: title,
        id: this.idGenerator()
      });
      this.updateStorage();
    },
    removeTask(index) {
      this.tasks.splice(index, 1);
      this.updateStorage();
    },
    updateStorage() {
      localStorage.setItem("tasks", JSON.stringify(this.tasks));
    }
  }
};
</script>

