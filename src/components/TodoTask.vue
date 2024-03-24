<template>
  <li class="task" v-if="showTask">
    <div class="task-name">
      <!-- checkbox -->
      <div class="checkbox-wrapper-12" @click="checkTask">
        <div class="cbx">
          <input type="checkbox" id="cbx-12" :checked="taskObj.checked" @change="checkTask" />
          <label for="cbx-12"></label>
          <svg fill="none" viewBox="0 0 15 14" height="14" width="15">
            <path d="M2 8.36364L6.23077 12L13 2"></path>
          </svg>
        </div>

        <svg version="1.1" xmlns="http://www.w3.org/2000/svg">
          <defs>
            <filter id="goo-12">
              <feGaussianBlur
                result="blur"
                stdDeviation="4"
                in="SourceGraphic"
              ></feGaussianBlur>
              <feColorMatrix
                result="goo-12"
                values="1 0 0 0 0  0 1 0 0 0  0 0 1 0 0  0 0 0 22 -7"
                mode="matrix"
                in="blur"
              ></feColorMatrix>
              <feBlend in2="goo-12" in="SourceGraphic"></feBlend>
            </filter>
          </defs>
        </svg>
      </div>
      <!-- checkbox -->
      <input
        type="text"
        class="task-name-li"
        :class="{ taskcheked: ischecked, readOnly: !isReadOnly }"
        :value="taskObj.task"
        :readonly="isReadOnly"
        v-model="taskObj.task"
      />
    </div>
    <div class="task-edit">
      <iconCheck @click="confirmEditingTask" v-if="!isReadOnly"></iconCheck>
      <iconPen @click="editTasks" v-if="isReadOnly"></iconPen>
      <iconTrash @click="deleteTask"></iconTrash>
    </div>
  </li>
</template>

<script>
import iconPen from "./icons/iconPen.vue";
import iconTrash from "./icons/iconTrash.vue";
import iconCheck from "./icons/iconCheck.vue";

export default {
  name: "TodoTask",
  components: {
    iconPen,
    iconTrash,
    iconCheck,
  },
  props: ["taskObj", "taskIndex"],
  data() {
    return {
      ischecked: false,
      showTask: true,
      isReadOnly: true,
    };
  },
  methods: {
    checkTask() {
      this.$emit('checkTaskinArray',[this.taskIndex, this.ischecked])
      if (!this.ischecked) {
        this.ischecked = true;
      } else if (this.ischecked) {
        this.ischecked = false;
      }
    },
    deleteTask() {
      this.$emit('deleteTaskFromArray', this.taskIndex)
      this.showTask = false;
    },
    editTasks() {
      this.isReadOnly = false;
    },
    confirmEditingTask() {
      this.$emit('editTaskInArray', [this.taskIndex, this.taskObj.task])
      this.isReadOnly = true;
    },
  },
};
</script>

<style scoped>
.task {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: white;
  border-radius: 4px;
  cursor: pointer;
  margin-top: 8px !important;
  padding: 12px 20px 12px 16px;
  text-align: left;
  font-size: 16px;
  box-sizing: border-box;
  transform: translateY(2px);
}
.task-name {
  display: flex;
  justify-content: flex-start;
  align-items: center;
  position: relative;
  overflow-wrap: break-word;
  flex: 1;
}
.task-name-li {
  width: 100%;
  border: none;
  border-radius: 4px;
  margin-left: 6px !important;
  padding: 6px;
  color: #555;
}
.task-edit {
  display: flex;
  justify-content: flex-end;
  align-items: center;
  gap: 15px;
}
.taskcheked {
  text-decoration: line-through;
  opacity: 0.6;
}
.readOnly {
  border: 2px dashed var(--clr-dark);
}
/* checkbox */
.checkbox-wrapper-12 {
  position: relative;
}
.checkbox-wrapper-12 > svg {
  position: absolute;
  top: -130%;
  left: -170%;
  width: 110px;
  pointer-events: none;
}
.checkbox-wrapper-12 * {
  box-sizing: border-box;
}
.checkbox-wrapper-12 input[type="checkbox"] {
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
  -webkit-tap-highlight-color: transparent;
  cursor: pointer;
  margin: 0;
}
.checkbox-wrapper-12 input[type="checkbox"]:focus {
  outline: 0;
}
.checkbox-wrapper-12 .cbx {
  width: 24px;
  height: 24px;
  top: calc(100px - 12px);
  left: calc(100px - 12px);
}
.checkbox-wrapper-12 .cbx input {
  position: absolute;
  top: 0;
  left: 0;
  width: 24px;
  height: 24px;
  border: 2px solid #bfbfc0;
  border-radius: 50%;
}
.checkbox-wrapper-12 .cbx label {
  width: 24px;
  height: 24px;
  background: none;
  border-radius: 50%;
  position: absolute;
  top: 0;
  left: 0;
  transform: trasnlate3d(0, 0, 0);
  pointer-events: none;
}
.checkbox-wrapper-12 .cbx svg {
  position: absolute;
  top: 5px;
  left: 4px;
  z-index: 1;
  pointer-events: none;
}
.checkbox-wrapper-12 .cbx svg path {
  stroke: #fff;
  stroke-width: 3;
  stroke-linecap: round;
  stroke-linejoin: round;
  stroke-dasharray: 19;
  stroke-dashoffset: 19;
  transition: stroke-dashoffset 0.3s ease;
  transition-delay: 0.2s;
}
.checkbox-wrapper-12 .cbx input:checked + label {
  animation: splash-12 0.6s ease forwards;
}
.checkbox-wrapper-12 .cbx input:checked + label + svg path {
  stroke-dashoffset: 0;
}
@-moz-keyframes splash-12 {
  40% {
    background: var(--clr-dark);
    box-shadow: 0 -18px 0 -8px var(--clr-dark), 16px -8px 0 -8px var(--clr-dark),
      16px 8px 0 -8px var(--clr-dark), 0 18px 0 -8px var(--clr-dark),
      -16px 8px 0 -8px var(--clr-dark), -16px -8px 0 -8px var(--clr-dark);
  }

  100% {
    background: var(--clr-dark);
    box-shadow: 0 -36px 0 -10px transparent, 32px -16px 0 -10px transparent,
      32px 16px 0 -10px transparent, 0 36px 0 -10px transparent,
      -32px 16px 0 -10px transparent, -32px -16px 0 -10px transparent;
  }
}
@-webkit-keyframes splash-12 {
  40% {
    background: var(--clr-dark);
    box-shadow: 0 -18px 0 -8px var(--clr-dark), 16px -8px 0 -8px var(--clr-dark),
      16px 8px 0 -8px var(--clr-dark), 0 18px 0 -8px var(--clr-dark),
      -16px 8px 0 -8px var(--clr-dark), -16px -8px 0 -8px var(--clr-dark);
  }

  100% {
    background: var(--clr-dark);
    box-shadow: 0 -36px 0 -10px transparent, 32px -16px 0 -10px transparent,
      32px 16px 0 -10px transparent, 0 36px 0 -10px transparent,
      -32px 16px 0 -10px transparent, -32px -16px 0 -10px transparent;
  }
}
@-o-keyframes splash-12 {
  40% {
    background: var(--clr-dark);
    box-shadow: 0 -18px 0 -8px var(--clr-dark), 16px -8px 0 -8px var(--clr-dark),
      16px 8px 0 -8px var(--clr-dark), 0 18px 0 -8px var(--clr-dark),
      -16px 8px 0 -8px var(--clr-dark), -16px -8px 0 -8px var(--clr-dark);
  }

  100% {
    background: var(--clr-dark);
    box-shadow: 0 -36px 0 -10px transparent, 32px -16px 0 -10px transparent,
      32px 16px 0 -10px transparent, 0 36px 0 -10px transparent,
      -32px 16px 0 -10px transparent, -32px -16px 0 -10px transparent;
  }
}
@keyframes splash-12 {
  40% {
    background: var(--clr-dark);
    box-shadow: 0 -18px 0 -8px var(--clr-dark), 16px -8px 0 -8px var(--clr-dark),
      16px 8px 0 -8px var(--clr-dark), 0 18px 0 -8px var(--clr-dark),
      -16px 8px 0 -8px var(--clr-dark), -16px -8px 0 -8px var(--clr-dark);
  }
  100% {
    background: var(--clr-dark);
    box-shadow: 0 -36px 0 -10px transparent, 32px -16px 0 -10px transparent,
      32px 16px 0 -10px transparent, 0 36px 0 -10px transparent,
      -32px 16px 0 -10px transparent, -32px -16px 0 -10px transparent;
  }
}
/* checkbox */
</style>
