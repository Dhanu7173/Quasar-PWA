<template>
  <div class="container">
    <div class="todo-app">
      <div class="app-title">
        <h2>To-do app</h2>
        <q-icon size="xl"  name="class" />
      </div>
      <div class="flex row">
        <input
          style="width:60%"
          id="input-box"
          placeholder="add your tasks"
          v-model="newTask"
          @keyup.enter="addTask"
        />
        <q-btn @click="addTask" rounded color="primary">Add Task</q-btn>
      </div>
      <ul id="list-container">
        <li
          v-for="(task, index) in tasks"
          :key="index"
          @click="toggleTask(index)"
          :class="{ 'checked': task.checked }"
        >
          {{ task.text }}
          <span @click="removeTask(index)">x</span>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTask: '',
      tasks: [],
    };
  },
  mounted() {
    this.showTask();
  },
  methods: {
    addTask() {
      if (this.newTask === '') {
        alert('You must write something!');
      } else {
        this.tasks.push({ text: this.newTask, checked: false });
        this.newTask = '';
        this.saveData();
      }
    },
    toggleTask(index) {
      this.tasks[index].checked = !this.tasks[index].checked;
      this.saveData();
    },
    removeTask(index) {
      this.tasks.splice(index, 1);
      this.saveData();
    },
    saveData() {
      localStorage.setItem('data', JSON.stringify(this.tasks));
    },
    showTask() {
      const savedData = localStorage.getItem('data');
      if (savedData) {
        this.tasks = JSON.parse(savedData);
      }
    },
  },
};
</script>

<style scoped>
.container {
  min-height: 100%;
  background: linear-gradient(135deg, #153677, #4e085f);
  padding: 10px;
  display: flex;
  justify-content: center;
  align-items: center;
}

.todo-app {
  width: 100%;
  max-width: 540px;
  background-color: #fff;
  padding: 40px 30px 40px;
  border-radius: 10px;
  display: flex;
  flex-direction: column;
  align-items: left;
  gap: 2rem;
}

.app-title {
  display: flex;
  gap: 1rem;
  align-items: center;
}

.app-title h2,
.app-title q-icon {
  color: #002765;
}

.app-title q-icon {
  font-size: 26px;
}

.row {
  display: flex;
  align-items: center;
  justify-content: space-between;
  background-color: #edeef0;
  border-radius: 30px;
}

input {
  width: 100%;
  border: none;
  outline: none;
  background-color: transparent;
  padding: 12px;
  font-size: 17px;
  padding-left: 20px;
}

q-btn {
  border: none;
  cursor: pointer;
  outline: none;
  padding: 15px 50px;
  border-radius: 30px;
  font-size: 18px;
}

ul {
  list-style: none;
}

ul li {
  font-size: 17px;
  padding: 12px 8px 12px 50px;
  margin-top: 5px;
  user-select: none;
  cursor: pointer;
  position: relative;
}

ul li::before {
  position: absolute;
  content: '';
  width: 24px;
  height: 24px;
  border-radius: 50%;
  left: 0;
  border: 2px solid #ff5945;
}

ul .checked {
  color: #555;
  text-decoration: line-through;
}

ul .checked::before {
  background-color: #ff5945;
}

span {
  position: absolute;
  right: 0;
  top: 50%;
  transform: translateY(-50%);
  width: 30px;
  height: 30px;
  border-radius: 50%;
  display: flex;
  justify-content: center;
  align-items: center;
  color: #555;
  font-size: 18px;
  transition: all 0.2s ease;
}

span:hover {
  background-color: #c9c9c9;
  color: #fff;
}
</style>
