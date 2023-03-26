<template>
  <div class="timer-block" :style="{ '--colorVar': color }">
    <div class="timer-block__time">
      {{
        (second >= 3600 ? (hours % 60 < 10 && "0") + hours + ":" : "") +
        (second >= 60 ? (minutes % 60 < 10 && "0") + minutes + ":" : "") +
        ((second % 60 < 10 && "0") + (second % 60))
      }}
    </div>
    <div class="timer-block__buttons">
      <img
        @click="startTimer()"
        :src="active ? 'images/pause.svg' : 'images/treugol.svg'"
        alt="start/stop"
        class="timer-block__start"
      />
      <div class="timer-block__reset" @click="killTimer()"></div>
    </div>
    <div class="timer-block__decore"></div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      second: 0,
      allminutes: 0,
      active: false,
      timerInterval: null,
      colorVar: "#9e9e9e",
    };
  },
  computed: {
    minutes() {
      let computedMinutes = Math.floor(this.second / 60);
      this.allminutes = computedMinutes;
      if (computedMinutes >= 60) {
        computedMinutes = computedMinutes % 60;
      }
      return computedMinutes;
    },

    hours() {
      let computedHours = Math.floor(this.allminutes / 60);
      return computedHours;
    },
    
    color() {
      if (this.active) {
        return "#FFFFFF";
      } else {
        return "#9e9e9e";
      }
    },
  },
  created() {
    this.startTimer();
  },
  methods: {
    startTimer() {
      if (!this.active) {
        this.active = true;
        this.timerInterval = setInterval(() => {
          this.second++;
        }, 1000);
      } else {
        this.stopTimer();
      }
    },
    stopTimer() {
      this.active = false;
      clearInterval(this.timerInterval);
    },
    killTimer() {
      this.stopTimer();
      this.second = 0;
    },
  },
};
</script>

<style lang="scss">
.timer-block {
  display: grid;
  grid-template-columns: 1fr;
  grid-template-rows: 1fr 1fr;
  gap: 1px;
  position: relative;
  width: 225px;
  height: 120px;
  background: #696969;
  color: var(--colorVar);

  * {
    transition: all 0.2s ease;
  }

  &__time {
    font-weight: 400;
    font-size: 22px;
    line-height: 22px;
  }

  &__time {
    font-weight: 400;
    font-size: 22px;
    line-height: 22px;
  }

  &__decore {
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
    width: 100%;
    height: 1px;
    background: var(--colorVar);
  }

  &__buttons {
    display: flex;
    width: 85px;
    justify-content: space-between;
  }

  &__start {
    height: fit-content;
    cursor: pointer;
  }
  &__time,
  &__buttons {
    align-self: center;
    justify-self: center;
  }

  &__reset {
    padding: 10px;
    background: var(--colorVar);
    cursor: pointer;
  }
}
</style>