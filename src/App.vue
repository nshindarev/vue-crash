<template>
  <div class="container">
    <Header title="Task Tracker" />
    <Tasks @toggle-reminder="toggleReminder" @delete-task="deleteTask" :tasks="tasks" />
  </div>
</template>

<script>
import Header from './components/Header'
import Tasks from './components/Tasks'

export default {
  name: 'App',
  components: {
    Header,
    Tasks,
  },
  methods:{
    deleteTask (id){
      if (confirm('Are you sure?')){
        this.tasks = this.tasks.filter((task) => task.id !== id)
      }
    },

    toggleReminder(id){
      this.tasks = this.tasks.map((task) => 
        task.id === id ? { ...task, reminder: !task.reminder} : task)
    },
  },

  // lifecycle methods:
  data() {
    return {
      tasks: []
    }
  },
  created() {
    this.tasks = [
      {
        id: 1,
        text: "Ikamet appointment booking",
        day: "tomorrow",
        reminder: true,
      },
      {
        id: 2,
        text: "Visa receive",
        day: "9 Jan 2023",
        reminder: true,
      },
      {
        id: 3,
        text: "Money transfer",
        day: "tomorrow",
        reminder: false,
      },
      {
        id: 4,
        text: "Book hotel for friends",
        day: "tomorrow",
        reminder: false
      },
      {
        id: 5,
        text: "Finish Vue course",
        day: "25 Dec 2022",
        reminder: false,
      },
    ]
  }
}

</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: 'Poppins', sans-serif;
}

.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}

.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}

.btn:focus {
  outline: none;
}

.btn:active {
  transform: scale(0.98);
}

.btn-block {
  display: block;
  width: 100%;
}
</style>
