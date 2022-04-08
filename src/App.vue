<template>
  <div class="container">
    <div class="task_control">
      <task-control v-on:timeChange="onTimeChange" v-bind:actveTask="activeTask" v-bind:time="totalTime"/>
    </div>
    <div class="project_selection">
      Task
    </div>
    <div class="tasks">
      <tasks v-bind:tasks="tasks" v-bind:activeTaskId="activeTask?.id" v-on:change="changeTask"/>
      <form v-on:submit.prevent="createTask">
        <input class="input_task" type="text" v-model="title">
        <button class="btn" v-bind:disabled="this.title === ''">+</button>
      </form>
   
    </div>

  </div>
</template>

<script>

import Tasks from '@/components/Tasks'
import TaskControl from '@/components/TaskControl'
// import { Task } from './models'

export default {
  name: "App",
  mounted() {
    this.countTotalTime()
  },
  components: {
    Tasks,
    TaskControl
  },
  data () {
    return {
      tasks: JSON.parse(localStorage.getItem('tasks')) || [],
      title: '',
      activeTask: undefined,
      totalTime: 0,
    }
  },

  methods: {
    changeTask(task) {
      this.activeTask = task;

    },
    onTimeChange(time) {
      this.activeTask.timer = time;
      this.countTotalTime()
      localStorage.setItem('tasks', JSON.stringify(this.tasks))
    },
    countTotalTime(){
      let count = 0;
      for (let i = 0; i < this.tasks.length; i++) {
        count += this.tasks[i].timer;
      }
      this.totalTime = count;
    },
    createTask(){
      const task = {id: this.tasks.length, title: this.title, timer: 0}
      this.tasks.push(task);
      localStorage.setItem('tasks', JSON.stringify(this.tasks))
      this.title = '';
    }
  }

};

</script>

<style>
* {
  box-sizing: border-box;
}

body {
  display: flex;
  justify-content: center;
}
.container {
  display: flex;
  flex-direction: column;
  width: 500px;
  height: auto;
  min-height: 500px;
  border: 2px solid black;
  margin-top: 20px;
}
.task_control {
  display: flex;

  width: auto;
  height: auto;
  margin: 5px;
}
.project_selection {
  border: 1px solid black;
  width: auto;
  height: 50px;
  margin: 5px;
}
.tasks {
  display: flex;
  flex-direction: column;
  border-radius: 3px;
  width: auto;
  height: auto;
  margin: 5px;
}
.input_task {
  height: 30px;
}
.btn {
  margin-left: 5px;
  height: 30px;
  width: 30px;
  background: none;
  background-color: lightgray;
  border: 1px solid gray;
  border-radius: 3px;
  font-size: 20px;
  transition: background-color 150ms ease;
  cursor: pointer;
}
.btn:hover {
    background: gray;
}
form {
  display: flex;
  margin-top: 10px;
}

</style>
