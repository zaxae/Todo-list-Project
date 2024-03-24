<template>
  <div class="pomodoro">
    <div class="pomodoro-section">
      <div class="pomo-break">
        <button
          :class="{ active: activeButton === 'pomodoro' }"
          @click.prevent="toggleButton('pomodoro')"
        >
          Pomodoro
        </button>
        <button
          :class="{ active: activeButton === 'break' }"
          @click="toggleButton('break')"
        >
          Break
        </button>
      </div>
      <div class="pomo-timer">
        <span>{{
          `${minutes < 10 ? "0" + minutes : minutes}:${
            seconds < 10 ? "0" + seconds : seconds
          }`
        }}</span>
      </div>
      <div class="pomo-on-off">
        <button
          class="pomo-on-off-btn"
          :class="{ pomoOnOffActive: isBtnOn }"
          @click.prevent="startTimer"
        >
          {{ startStop ? "Start" : "Stop" }}
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "TodoPomodoro",
  props: ['pomodoroTime','breakTime'],
  data() {
    return {
      activeButton: "pomodoro",
      minutes: this.pomodoroTime,
      seconds: 0,
      timer: null,
      startStop: true,
      isBtnOn: false,
    };
  },
  methods: {
    toggleButton(button) {
      this.activeButton = button;
      if (button === "pomodoro") {
        this.minutes = this.pomodoroTime;
        this.seconds = 0;
        this.startStop = true;
        this.isBtnOn = false;
        clearInterval(this.timer);
      } else if (button === "break") {
        this.minutes = this.breakTime;
        this.seconds = 0;
        this.startStop = true;
        this.isBtnOn = false;
        clearInterval(this.timer);
      }
    },
    startTimer() {
      if (this.startStop) {
        this.startStop = false;
        this.isBtnOn = true;
        this.timer = setInterval(() => {
          if (this.seconds === 0) {
            if (this.minutes === 0) {
              clearInterval(this.timer);
            } else {
              this.minutes--;
              this.seconds = 59;
            }
          } else {
            this.seconds--;
          }
        }, 1000);
      } else if (!this.startStop) {
        this.startStop = true;
        this.isBtnOn = false;
        clearInterval(this.timer); // Clear the timer when the component is destroyed to prevent memory leaks
      }
    },
  },
  beforeDestroy() {
    clearInterval(this.timer); // Clear the timer when the component is destroyed to prevent memory leaks
  },
};
</script>

<style scoped>
.pomodoro {
  width: 100%;
}
.pomodoro-section {
  width: 100% !important;
  max-width: 480px;
  margin: 40px auto !important;
  background-color: rgba(255, 255, 255, 0.1);
  padding: 20px 0px 30px;
  border-radius: 6px;
  text-align: center;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  gap: 20px;
}
.pomo-break {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 5px;
  margin: 0 0 -10px !important;
}
.pomo-break button {
  margin: 0;
  border-radius: 4px;
  font-size: 16px;
  padding: 2px 12px;
  height: 28px;
  cursor: pointer;
  box-shadow: none;
  color: white;
  opacity: 1;
  letter-spacing: 0.3px;
}
.pomo-break button:active {
  transform: translateY(2px);
  box-shadow: none;
}
.active {
  background: none rgba(0, 0, 0, 0.15);
  font-weight: 600;
}
.pomo-timer {
  font-size: 120px;
  font-weight: 600;
  letter-spacing: 1px;
}
.pomo-on-off-btn {
  cursor: pointer;
  border: none;
  padding: 0px 12px;
  border-radius: 4px;
  box-shadow: rgb(235, 235, 235) 0px 6px 0px;
  font-size: 22px;
  text-transform: uppercase;
  height: 55px;
  color: var(--clr-dark);
  font-weight: bold;
  width: 200px;
  background-color: white;
  transition: all 0.1s ease-in-out 0s;
}
.pomoOnOffActive {
  box-shadow: none;
  transform: translateY(6px);
}
</style>
