<template>
  <div>
    <div class="timer">
      <div
        class="number-box"
        v-for="(number, index) in dividedTime"
        :key="index"
      >
        {{ dividedTime[index] }}
      </div>
    </div>
    <div class="actions">
      <button @click="start">Start</button>
      <button @click="pause">Pause</button>
      <button @click="set">Set</button>
      <button @click="finish">Finish</button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    startedTime: {
      type: Number,
      required: true,
    },
  },
  data() {
    return {
      timerTime: 0,
      paused: false,
      inProcess: false,
    };
  },
  mounted() {
    this.timerTime = this.startedTime;
  },
  methods: {
    start() {
      if (this.timerTime <= 0) return;
      if (this.paused) {
        this.paused = false;
        return;
      }

      setInterval(() => {
        this.inProcess = true;
        if (!this.paused && this.timerTime > 0) this.timerTime--;
      }, 1000);
    },
    pause() {
      if (this.inProcess) this.paused = true;
    },
    finish() {
      this.timerTime = 0;
    },
    set() {
      this.$emit("edit", this.timerTime);
    },
  },
  computed: {
    dividedTime() {
      let result = [0, 0, 0, 0];
      let seconds = (this.timerTime % 60).toString();
      let minutes = Math.floor(this.timerTime / 60).toString();
      let secondsArray = seconds.split("");
      if (secondsArray.length == 1) result[3] = secondsArray[0];
      else {
        result[3] = secondsArray[1];
        result[2] = secondsArray[0];
      }
      let minutesArray = minutes.split("");
      if (minutesArray.length == 1) result[1] = minutesArray[0];
      else {
        result[1] = minutesArray[1];
        result[0] = minutesArray[0];
      }
      return result;
    },
  },
};
</script>

<style scoped>
.actions {
  margin-top: 20px;
}
.actions button {
  background-color: #fff;
  color: rgb(78, 172, 78);
  border: 1px solid rgb(78, 172, 78);
  border-radius: 5px;
  height: 40px;
  font-size: 24px;
  cursor: pointer;
  margin-right: 20px;
  min-width: 200px;
}
.actions button:hover {
  color: rgb(61, 136, 61);
}
.timer {
  display: flex;
  justify-content: center;
}
.timer .number-box {
  font-size: 40px;
  border: 1px solid rgb(61, 136, 61);
  padding: 8px 10px;
  border-radius: 8px;
  color: rgb(61, 136, 61);
  margin-right: 10px;
}
</style>