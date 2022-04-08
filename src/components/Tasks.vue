<template>
  <div>
    <ul class="tasks" v-if="tasks.length > 0">
      <li class="task"
        v-for="task in tasks"
        v-bind:key="task.id"
        v-on:click="onTaskChange(task)"
        v-bind:class="{active: task.id === activeTaskId}"
      >
        <span>{{ task.title }}</span> <span>{{ task.timer }}</span> 
      </li>
    </ul>
    <div v-else>Задач нет</div>
  </div>
</template>




<script>
export default {





  props: {
    tasks: {
      type: Array,
      default: () => [],
    },
    activeTaskId: {
      type: Number,
      default: -1,
    },
  },
  methods: {
    onTaskChange(task) {
      this.$emit("change", task);
    //   console.log(task);
    },
  },
};






</script>

<style scoped>
.tasks {
  flex-direction: column;
  justify-content: center;
  list-style: none;
  margin: 0;
  padding: 1px;
}
li {
  border: 1px solid brown;
  padding: 5px;
  margin-top: 5px;
  transition: background-color 150ms ease;
  cursor: pointer;
}
li:not(.active):hover {
  background: gray;
}
.active {
    background: lightblue;
}
.task {
  display: flex;
  justify-content: space-between;
}
</style>
