<template>
  <task
     :tasks = "taskList"
     @clear_Task="handleClearTask()"
     @save_Task="handleSaveTask()"
  />
</template>

<script>
import task from "./components/Task.vue"
export default {
  name: 'App',
  components: {
    task,
  },
  data() {
    return {
      taskList: [
        { 
          id: 1,
          title: 'Learn Python',
          isCompleted: false,
        },
        { 
          id: 2,
          title: 'Learn Data Structure and Algorithm', 
          isCompleted: false,
        },
        { 
          id: 3,
          title: 'Learn MEVN Stack',
          isCompleted: false,
        },
      ],
    }
  },
  methods: {
    handleClearTask() {
      this.taskList = []
      this.handleSaveTask();
    },
    handleSaveTask() {
      localStorage.setItem('taskList', JSON.stringify(this.taskList));
    },
  },
  mounted() {
    const getTasks = localStorage.getItem('taskList');
      if(getTasks) {
        this.taskList = JSON.parse(getTasks);
      }
    },
}
</script>
