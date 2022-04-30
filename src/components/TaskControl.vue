<template>
  <div class="control">
    <div v-if="actveTask">
      <span>{{ actveTask.title }}</span>
    </div>
    <div v-else>Выбери задачу</div>
    <button
      class="btn"
      v-on:click="startTimer"
      v-bind:disabled="actveTask === undefined"
    >
      Play
    </button>
    <button class="btn" v-on:click="stopTimer">Stop</button>
    <span>{{ time }}</span>
  </div>
</template>

<script>
export default {
  props: {
    actveTask: {
      type: Object,
    },
    time: {
      type: Number,
      default: 0,
    },
  },
  methods: {
    startTimer() {
      this.stopTimer();
      this.interval = setInterval(() => {
        this.$emit("timeChange", this.actveTask.timer + 1);
      }, 1000);
    },
    stopTimer() {
      clearInterval(this.interval);
    },
  },
};
</script>

<style scoped>
.control {
  display: flex;
  flex: 1;
  padding: 5px;
  justify-content: space-between;
}
.btn {
  margin-left: 5px;
  height: 30px;
  width: auto;
  background-color: lightgray;
  border: 1px solid gray;
  border-radius: 3px;
  font-size: 15px;
}
.btn:hover {
  background: gray;
}
</style>
