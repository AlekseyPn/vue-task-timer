<template>
  <div class="task-item">
    <span class="task-item__position-number">{{ positionNumber }}</span>
    <span class="task-item__title" :title="item.title">{{ item.title }}</span>
    <span class="task-item__timer">{{ timeValue }}</span>
    <div class="row task-item__controls">
      <button class="task-item__control-button" :tabindex="positionNumber" @click="startTimer">
        <i class="fas fa-play"></i>
      </button>
      <button class="task-item__control-button" :tabindex="positionNumber" @click="stopTimer">
        <i class="fas fa-pause"></i>
      </button>
      <button class="task-item__control-button" :tabindex="positionNumber" @click="resetTimer">
        <i class="fas fa-redo"></i>
      </button>
      <button class="task-item__control-button" :tabindex="positionNumber" @click="removeTask">
        <i class="fas fa-trash"></i>
      </button>
    </div>
  </div>
</template>
    
<script>
const TIME_UNITS_TRESHOLDS = {
  forTenUnit: 9,
  forHourUnits: 23,
  forMinutesAndSeconds: 59
};
export default {
  props: {
    item: {
      type: Object
    },
    index: {
      type: Number
    }
  },
  data() {
    return {
      seconds: "00",
      minutes: "00",
      hours: "00",
      isStarted: false,
      timerInterval: null,
      propsForReset: ["seconds", "minutes", "hours"]
    };
  },
  computed: {
    timeValue() {
      return `${this.hours}:${this.minutes}:${this.seconds}`;
    },
    positionNumber() {
      return `${this.index + 1}.`;
    }
  },
  methods: {
    click() {
      this.$emit("removeTask");
    },
    isLessTenTime(value) {
      return +value < TIME_UNITS_TRESHOLDS.forTenUnit;
    },
    isMaxTimeValue(
      value,
      maxValue = TIME_UNITS_TRESHOLDS.forMinutesAndSeconds
    ) {
      return +value > maxValue;
    },
    reset() {
      clearInterval(this.timerInterval);
      this.timerInterval = null;
      this.isStarted = false;
    },
    prependZero(key) {
      return () => {
        this[key] = this[key] < 10 ? `0${this[key]}` : this[key];
      };
    },
    incrementValue(key) {
      return () => {
        this[key] += 1;
      };
    },
    checkMaxValue(key, valueForCompare) {
      return () => {
        this[key] = this.isMaxTimeValue(this[key], valueForCompare)
          ? "00"
          : this[key];
      };
    },
    taskTimer() {
      this.seconds = this.isLessTenTime(this.seconds)
        ? "0" + (+this.seconds + 1)
        : +this.seconds + 1;

      if (this.isMaxTimeValue(this.seconds)) {
        this.seconds = "00";

        this.minutes = this.isLessTenTime(this.minutes)
          ? "0" + (+this.minutes + 1)
          : +this.minutes + 1;
      }

      if (this.isMaxTimeValue(this.minutes)) {
        this.minutes = "00";

        this.hours = this.isLessTenTime(this.hours)
          ? "0" + (+this.hours + 1)
          : +this.hours + 1;

        if (
          this.isMaxTimeValue(this.hours, TIME_UNITS_TRESHOLDS.forHourUnits)
        ) {
          this.hours = "00";
        }
      }
    },
    startTimer() {
      if (!this.isStarted) {
        this.timerInterval = setInterval(this.taskTimer, 1000);
        this.isStarted = true;
      }
    },
    stopTimer() {
      this.reset();
    },
    resetTimer() {
      this.reset();
      this.propsForReset.forEach(it => (this[it] = "00"));
    },
    removeTask() {
      this.$emit("removeTask", this.index);
    }
  }
};
</script>
<style lang="scss" scoped>
.task-item {
  display: grid;
  grid-template-rows: 100%;
  grid-template-columns: 5% 1fr 1fr 1fr;
  grid-gap: 10px;
  align-content: start;
  margin-bottom: 10px;

  &__title {
    max-width: 150px;
    text-overflow: ellipsis;
    overflow: hidden;
    font-size: 20px;
  }

  &__timer {
    justify-self: center;
    align-self: start;
  }

  &__time,
  &__position-number {
    font-size: 20px;
  }

  &__controls {
    align-self: start;
    flex-wrap: nowrap;
    justify-content: flex-start;
  }

  &__control-button {
    width: 40px;
    height: 40px;
    margin-left: 10px;
    color: #fff;
    background-color: #7de591;
    border: none;
    &:focus,
    &:hover {
      outline: none;
      border: 1px solid #0d8a82;
    }
  }
}
</style>


