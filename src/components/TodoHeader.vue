<template>
  <header>
    <div class="logo">
      <span>PomoDoList</span>
    </div>
    <div class="info">
      <todo-btn @click="settingClicked"><icon-gear></icon-gear><span>Setting</span></todo-btn>
      <div class="setting-temp" v-if="isSettingClicked">
        <div class="setting-header">
          <span class="setting-header-text">Setting</span>
          <span class="setting-header-close" @click="settingClicked">✖</span>
        </div>
        <div class="setting-timer">
          <h3 class="timer-text">Time (minutes)</h3>
          <div class="timer-inputs">
            <div class="pomo">
              <label for="pomodoro">Pomodoro</label>
              <input type="number" v-model.number="pomodoroTime" />
            </div>

            <div class="brk">
              <label for="break">Break</label>
              <input type="number" v-model.number="breakTime" />
            </div>
          </div>
        </div>
        <div class="save-settings">
          <button @click="saveToPomoComponent">Save</button>
        </div>
      </div>
      <todo-btn><icon-user></icon-user><span>Login</span></todo-btn>
    </div>
  </header>
</template>

<script>
import TodoBtn from "./TodoBtn.vue";
import iconGear from "./icons/iconGear.vue";
import iconUser from "./icons/iconUser.vue";

export default {
  name: "TodoHeader",
  components: {
    TodoBtn,
    iconGear,
    iconUser,
  },
  data() {
    return {
      isSettingClicked: false,
      pomodoroTime: 25,
      breakTime: 5
    }
  },
  methods: {
    settingClicked() {
      if (this.isSettingClicked === true) {
        this.isSettingClicked = false 
      } else {
        this.isSettingClicked = true
      }
    },
    saveToPomoComponent() {
      this.$emit('saveToPomoComponent', [this.pomodoroTime, this.breakTime])
      this.settingClicked()
    }
  }
};
</script>

<style scoped>
header {
  background-color: inherit;
  width: 100%;
  height: 60px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-bottom: 1.5px solid rgb(160, 62, 62);
}

.logo {
  font-size: 20px;
  font-weight: 500;
  letter-spacing: 0.5px;
}
.info {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 5px;
  position: relative;
}
.setting-temp {
  position: absolute;
  background-color: #fff;
  border-radius: 4px;
  top: 30px;
  right: 75px;
}
.setting-header {
  font-size: 13px;
  color: rgb(170, 170, 170);
  text-transform: uppercase;
  font-weight: 500;
  padding: 12px 8px;
  border-bottom: 1px solid rgb(238, 238, 238);
  text-align: center;
  cursor: pointer;
}
.setting-header-close {
  position: absolute;
  right: 20px;
  cursor: pointer;
}
.setting-timer {
  color: #444;
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 8px;
  flex-direction: column;
  padding: 10px 20px;
}
.brk {
  margin-top: 8px !important;
}
.save-settings {
  padding: 10px 20px 20px;
  text-align: right;
}
.save-settings button {
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
  padding: 4px 8px;
  min-width: 70px;
  background-color: rgb(34, 34, 34);
  border: 2px solid rgb(34, 34, 34);
  display: inline-block;
}
</style>
