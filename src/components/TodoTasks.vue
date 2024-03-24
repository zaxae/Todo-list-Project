<template>
  <div class="todo-tasks">
    <div class="tasks-setting">
      <span>Tasks</span>
      <div class="clear-all" @click="clearAll" v-if="clearBtnToggle">
        Clear All
        <icon-white-trash></icon-white-trash>
      </div>
    </div>
    <ul>
      <todo-task
        v-for="(task, index) in tasksArray"
        :key="index"
        :taskIndex="index"
        :taskObj="task"
        @deleteTaskFromArray="deleteTaskFromArray"
        @editTaskInArray="editTaskInArray"
        @checkTaskinArray="checkTaskinArray"
      ></todo-task>
    </ul>
    <div class="tasks-adding" @click="addingTask" v-if="isTaskAddOpen">
      <span>+ Add Task</span>
    </div>
    <div class="add-task-container" v-if="!isTaskAddOpen">
      <input type="text" v-model="taskInput" />
      <div class="cancel-save">
        <button class="cancel" @click="cancelTask">Cancel</button>
        <button class="save" @click="saveTask">Save</button>
      </div>
    </div>
  </div>
</template>

<script>
import IconWhiteTrash from "./icons/iconWhiteTrash.vue";
import IconTrash from "./icons/iconTrash.vue";
import TodoTask from "./TodoTask.vue";

export default {
  name: "TodoTasks",
  components: {
    TodoTask,
    IconTrash,
    IconWhiteTrash,
  },
  data() {
    return {
      tasksArray: [],
      clearBtnToggle: this.tasksArray === [] ? false : true,
      taskInput: "",
      isTaskAddOpen: true,
    };
  },
  methods: {
    addingTask() {
      this.taskInput = "";
      this.isTaskAddOpen = false;
    },
    saveTask() {
      if (this.taskInput.trim() === "") return;

      const newTask = {
        task: this.taskInput,
        checked: false,
      };
      this.tasksArray.push(newTask);
      this.isTaskAddOpen = true;
      this.saveData();
    },
    cancelTask() {
      this.isTaskAddOpen = true;
    },
    deleteTaskFromArray(i) {
      this.tasksArray.splice(i, 1);
      this.saveData();
    },
    clearAll() {
      this.tasksArray = [];
      this.saveData();
    },
    editTaskInArray([i, task]) {
      this.tasksArray[i].task = task;
      this.saveData();
    },
    checkTaskinArray([i, check]) {
      this.tasksArray[i].checked = check;
      this.saveData();
    },
    saveData() {
      localStorage.setItem("tasksArray", JSON.stringify(this.tasksArray));
    },
  },
  created() {
    // Retrieve data from localStorage
    const storedData = JSON.parse(localStorage.getItem("tasksArray"));
    if (storedData) {
      this.tasksArray = storedData;
    }
  },
};
</script>

<style scoped>
.tasks-setting {
  display: flex;
  align-items: center;
  justify-content: space-between;
  border-bottom: 2px solid rgba(255, 255, 255, 0.6);
  padding-bottom: 14px;
  margin-bottom: 15px !important;
}
.tasks-setting span {
  font-size: 18px;
  font-weight: 500;
}
.clear-all {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
  text-align: center;
  border-radius: 4px;
  cursor: pointer;
  opacity: 0.9;
  background: none rgba(255, 255, 255, 0.2);
  font-size: 13px;
  font-weight: 500;
  padding: 8px;
  letter-spacing: 0.2px;
}
.clear-all:active {
  transform: translateY(2px);
  box-shadow: none;
}
.tasks-adding {
  box-sizing: border-box;
  width: 100%;
  height: 64px;
  background-color: rgba(0, 0, 0, 0.1);
  font-size: 17px;
  border-radius: 8px;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
  opacity: 0.8;
  margin-top: 15px !important;
  border: 2px dashed rgba(255, 255, 255, 0.4);
  transition: 0.2s;
}
.tasks-adding:hover {
  opacity: 1;
}
.add-task-container {
  background-color: white;
  border-radius: 8px;
  text-align: left;
  margin-top: 12px;
  box-shadow: rgba(0, 0, 0, 0.15) 0px 10px 20px, rgba(0, 0, 0, 0.1) 0px 3px 6px;
  animation: 0.1s ease-in-out 0s 1 normal none running expand;
  overflow: hidden;
  margin-top: 15px !important;
}
.add-task-container input {
  width: 100%;
  border: none;
  border-radius: 8px 8px 0 0;
  padding: 26px 20px;
  font-size: 20px;
  box-shadow: none;
  color: rgb(85, 85, 85);
  box-sizing: border-box;
  font-weight: 600;
}
.cancel-save {
  padding: 8px 20px;
  text-align: right;
  border-bottom-left-radius: 8px;
  border-bottom-right-radius: 8px;
  background-color: rgb(239, 239, 239);
  display: flex;
  justify-content: flex-end;
  align-items: center;
}
.cancel {
  text-align: center;
  border-radius: 4px;
  cursor: pointer;
  opacity: 0.9;
  font-size: 14px;
  padding: 8px 12px;
  min-width: 70px;
  display: inline-block;
  margin-right: 14px !important;
  background: none;
  border: none;
  color: rgb(136, 136, 136);
  font-weight: 600;
  box-shadow: none;
}
.save {
  -webkit-box-align: center;
  align-items: center;
  -webkit-box-pack: center;
  justify-content: center;
  text-align: center;
  border-radius: 4px;
  cursor: pointer;
  box-shadow: rgba(0, 0, 0, 0.1) 0px 2px 2px;
  color: white;
  opacity: 0.9;
  font-size: 14px;
  font-weight: 600;
  padding: 8px 12px;
  min-width: 70px;
  background-color: rgb(34, 34, 34);
  border: 2px solid rgb(34, 34, 34);
  display: inline-block;
}
</style>
