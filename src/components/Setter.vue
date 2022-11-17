<template>
  <div class="setter">
    <div class="edit-box" v-for="(timeNumber, index) in timeArray" :key="index">
      <arrow-icon
        style="cursor: pointer"
        class="top"
        @click="plus(index)"
      ></arrow-icon>
      <div class="number-box">{{ timeNumber }}</div>
      <arrow-icon style="cursor: pointer" @click="minus(index)"></arrow-icon>
    </div>
  </div>
  <div class="actions">
    <button @click="set">Set</button>
    <button @click="clear">Clear</button>
  </div>
</template>

<script>
import ArrowIcon from "./ArrowIcon.vue";
export default {
  components: { ArrowIcon },
  props: {
    startedTime: {
      type: Number,
      required: true,
    },
  },
  data() {
    return {
      timerTime: 0,
      timeArray: [0, 0, 0, 0],
    };
  },
  mounted() {
    this.divide();
  },
  methods: {
    divide() {
      let seconds = (this.startedTime % 60).toString();
      let minutes = Math.floor(this.startedTime / 60).toString();
      let secondsArray = seconds.split("");
      if (secondsArray.length == 1) this.timeArray[3] = secondsArray[0];
      else {
        this.timeArray[3] = secondsArray[1];
        this.timeArray[2] = secondsArray[0];
      }
      let minutesArray = minutes.split("");
      if (minutesArray.length == 1) this.timeArray[1] = minutesArray[0];
      else {
        this.timeArray[1] = minutesArray[1];
        this.timeArray[0] = minutesArray[0];
      }
    },
    set() {
      let minutesString =
        this.timeArray[0].toString() + this.timeArray[1].toString();
      let minutes = +minutesString;
      let secondsString =
        this.timeArray[2].toString() + this.timeArray[3].toString();
      let seconds = +secondsString;
      this.$emit("set", minutes * 60 + seconds);
    },
    clear() {
      this.timeArray = [0, 0, 0, 0];
    },
    minus(index) {
      let value = this.timeArray[index];
      if (value > 0) value--;
      this.timeArray[index] = value;
    },
    plus(index) {
      let value = this.timeArray[index];
      if (index == 0 || index == 2) if (value == 5) return;
      if (index == 1 || index == 3) if (value == 9) return;
      value++;
      this.timeArray[index] = value;
    },
  },
};
</script>

<style scoped>
#file-loader{
  display: none;
}
.top {
  transform: rotateX(180deg);
}
.edit-box {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  margin-right: 10px;
}
.setter {
  display: flex;
  justify-content: center;
}
.number-box {
  font-size: 40px;
  border: 1px solid #3d883d;
  padding: 8px 10px;
  border-radius: 8px;
  color: rgb(61, 136, 61);
  user-select: none;
}
.actions {
  margin-top: 20px;
}
.actions button {
  user-select: none;
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
</style>