<template>
  <div class="container">
    <todo-header @saveToPomoComponent="saveToPomoComponent"></todo-header>
    <todo-pomodoro :pomodoroTime="inputForPomo" :breakTime="inputForBrk"></todo-pomodoro>
    <todo-tasks></todo-tasks>
  </div>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue';
import TodoPomodoro from './components/TodoPomodoro.vue';
import TodoTasks from './components/TodoTasks.vue';

export default {
  name: "App",
  components: {
    TodoHeader,
    TodoPomodoro,
    TodoTasks
  },
  data() {
    return {
      inputForPomo: 25,
      inputForBrk: 5,
    }
  },
  methods: {
    saveToPomoComponent([pomo, brk]) {
      this.inputForPomo = pomo
      this.inputForBrk = brk
    }
  }
}
</script>

<style scoped>
</style>