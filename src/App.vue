<template>
<div class="container">
 <Header :showAddTask = "showAddTask" title ="Task Tracker" @toggle-add-task="toggleAddTask" />
 <div v-if="showAddTask">
    <AddTask @add-task = "addTask" />
 </div>
  <!-- <showAddTask /> -->
  <!-- <Button text="Add Task " color="green" /> -->
  <div class="Task">
      <Tasks :tasks = "tasks" @delete-task = "deleteTask" @toggle-reminder="ToggleReminder"/>
  </div>
  
</div>
  <!-- <img alt="Vue logo" src="./assets/logo.png">
  <HelloWorld msg="Welcome to Your Vue.js App"/> -->
 
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import Header from './components/Header.vue'
// import Button from './components/Button.vue'
import Tasks from './components/Tasks.vue'
import AddTask from './components/AddTask.vue'
import showAddTask from './components/showAddTask.vue'
export default {
  name: 'App',
  components: {
    Header,
    AddTask,
    Tasks,
    showAddTask,
  },
  data(){
   return{
	  tasks:[],
    showAddTask: false
    }
  },
   
  methods:{
    addTask(task){
      this.tasks = [...this.tasks, task]
    },
    deleteTask(id){
      console.log('task',id)
      if(confirm('Are You Sure')){
        this.tasks = this.tasks.filter((task) => task.id !== id)
      }
    },
    ToggleReminder(id){
      // console.log(id)
      this.tasks = this.tasks.map((task) => task.id === id ? {...task, reminder : ! task.reminder } : task)
    },
    async fetchTasks(){
      const res = await fetch('http://localhost:3000/tasks')
      const data = await res.json()
      return data
    },
      async fetchTask(id){
      const res = await fetch(`http://localhost:3000/tasks/${id}`)
      const data = await res.json()
      return data
    },
    toggleAddTask(){
      this.showAddTask = !this.showAddTask
    }
    
  },
  async created(){
    this.tasks = await this.fetchTasks()
    // this.tasks = [
    //   {
    //     id: 1,
    //     text: 'Doctors Appointment',
    //     day: 'March 1st at 2:30pm',
    //     reminder: true,
    //   },
    //   {
    //     id:2,
    //     text: 'saasasas',
    //     day: 'March 2nd at 2:30pm',
    //     reminder: true,
    //   },
    //   {
    //     id:3,
    //     text: 'eweqeweqwe',
    //     day: 'March 3rd at 2:30pm',
    //     reminder: false,
    //   }
    // ]
  },
}
</script>

<style>
*{
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
.container{
  border: 1px solid black;
  max-width: 500px;
  margin: 30px auto;
  overflow: hidden;
  min-height: 300px;
  padding: 30px;
  border-radius: 5px;

}
.btn{
  display: block;
  background: #000;
  color: #fff;
  border:none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
}
.btn:focus{
  outline: none;
}
.btn:active{
  transform: scale(.90);
}
.btn-block{
  display: block;
  width: 100%;
}
.Task{
  display:inline-block;
}
/* #app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
} */
</style>
