<template>
  <div class="container">
    <div class="task">
      <div class="title">
        <h1>My Todo App 📋</h1>
      </div>
      <div class="form">
        <input type="text" placeholder="Enter new task" v-model="newTask" @keydown.enter="addTask">
        <button @click="addTask"><i class="fa-solid fa-plus"></i></button>
      </div>
      <div class="taskItems">
        <ul :class="{ completed: task.isCompleted }" @click="checkCompleted(task)" v-for="(task,index) in tasks" :key="index"> 
          <li>{{ task.title }}</li>
          <button @click="removeTask(index)"><i class="fa-regular fa-trash-can"></i></button>
        </ul>
      </div>
      <button class="clear" @click="clearAll">Clear All</button>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    tasks: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      newTask: '',
      isCompleted: false,
    }
  },
  methods: {
    addTask() {
      if(this.newTask) {
        this.tasks.push({
          title: this.newTask,
          isCompleted: false,
        });
        this.newTask = '';
        this.saveTasksLocalStorage();
      }
    },
    removeTask(index) {
      this.tasks.splice(index, 1);
      this.saveTasksLocalStorage();
    },
    clearAll() { 
      this.$emit("clear_Task")
      this.saveTasksLocalStorage();
    },
    checkCompleted(task) {
      task.isCompleted = !task.isCompleted;
      console.log(task.isCompleted);
      this.saveTasksLocalStorage();
    },
    saveTasksLocalStorage() {
      this.$emit("save_Task")
    },
  }
}
</script>
<style lang="css" scoped>
.container {
  display:flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}
.task {
  width: 400px;
  height: 400px;
  background-color:white;
  border-radius: 10px;
  padding:30px;
  box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.2);
}
h1 {
  font-size:22px;
  text-align: center;
}
.form {
  position:relative;
  margin-top:20px
}
.form input {
  width: 100%;
  height: 50px;
  font: 15px / 1.4 Poppins, sans-serif;
  padding: 15px;
  border-radius:10px;
  border: 1px solid transparent;
  transition: border-color 0.3s ease;
  background-color: #f5f5f5;
}
.form input:focus {
  border-color:#4ec5c1;
  outline:none;
}
.form button {
  background:none;
  color:#4ec5c1;;
  border:none;
  position:absolute;
  top:37%;
  right:20px;
  cursor:pointer;
}
.taskItems {
  padding: 0 10px;
  max-height: 200px;
  overflow-y: auto;
}
ul {
  list-style: none;
  display:flex;
  justify-content: space-between;
  margin-top:20px;
}
ul.completed {
  text-decoration: line-through;
}
ul button {
  background:none;
  cursor:pointer;
  border:none;
  outline:none;
}
.clear {
  border:none;
  outline:none;
  color:white;
  padding:10px;
  margin-top:20px;
  background-color:#4ec5c1;
  border-radius:10px;
  cursor: pointer;
  font-size:15px;
}
</style>