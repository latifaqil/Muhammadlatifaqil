<template>
    <div id="app">
      <h1>Todo List dalil</h1>
      <div class="input-container">
        <input type="text" v-model="newTask" placeholder="masukan data" />
        <button @click="addTask" class="addTask">Add</button>
      </div>
      <div class="list-container">
        <ul>
          <li v-for="(task, index) in filteredTasks" :key="index">
            <span :class="{ 'completed': task.completed }">{{ task.name }}</span>
            <div class="button-container">
              <button @click="toggleTask(index)">
                {{ task.completed ? 'Batal' : 'Selesai' }}
              </button>
              <button @click="removeTask(index)">Hapus</button>
            </div>
          </li>
        </ul>
      </div>
      <button @click="showOnlyCompleted = !showOnlyCompleted">
        {{ showOnlyCompleted ? 'ShowNotCompleted' : 'Show Completed' }}
      </button>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        tasks: [],
        newTask: '',
        showOnlyCompleted: false
      };
    },
    computed: {
      filteredTasks() {
        if (this.showOnlyCompleted) {
          return this.tasks.filter(task => task.completed);
        } else {
          return this.tasks;
        }
      }
    },
    methods: {
      addTask() {
        if (this.newTask.trim() !== '') {
          this.tasks.push({
            name: this.newTask,
            completed: false
          });
          this.newTask = '';
        }
      },
      removeTask(index) {
        this.tasks.splice(index, 1);
      },
      toggleTask(index) {
        this.tasks[index].completed = !this.tasks[index].completed;
      }
    }
  };
  </script>
  
  <style scoped>
  #app {
    background-color: #333;
    margin: auto;
    padding: 10px;
    max-width: 700px;
    display: flex;
    flex-direction: column;
    align-items: center; /* Mengatur posisi elemen secara horizontal (horizontal alignment) menjadi tengah */
    justify-content: center; /* Mengatur posisi elemen secara vertikal (vertical alignment) menjadi tengah */
    min-height: 100vh; /* Menyediakan tinggi minimum sesuai dengan tinggi viewport untuk memastikan konten tetap di tengah saat konten sedikit */
  }
  
  
  #app h1 {
    text-align: center;
    color: white;
    font-family: 'Courier New', Courier, monospace;
  }
  
  .input-container {
    text-align: center;
    margin-bottom: 10px;
  }
  
  #app input[type=text] {
    height: 40px;
    width: 200px;
    border-radius: 10px;
    font-family:monospace;
    padding-right: 5px;
  }
  
  #app .addTask{
    height: 45px;
    width: 45px;
    background-color:burlywood;
    border-radius: 10px;
    margin: 10px;
  }
  
  
  #app ul {
    list-style-type: none;
    padding: 0;
    margin: 0;
  }
  
  #app li {
    padding: 5px;
    align-items: center;
    display: flex;
  
  }
  
  .completed {
    text-decoration: line-through;
  }
  </style>