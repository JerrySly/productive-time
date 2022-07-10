<template>
  <div class="home">
    <h1>Productive Timer</h1>
    <setter v-if="editMode" @set="setTime" :startedTime="time"></setter>
    <timer v-else @edit="startEdit" :startedTime="time"></timer>
  </div>
</template>

<script>
import Timer from "@/components/Timer.vue";
import Setter from "@/components/Setter.vue"
export default {
  name: "HomeView",
  components: {
    Timer,
    Setter
  },
  data(){
    return{
      editMode: false,
      time: 0
    }
  },
  methods:{
    startEdit(value){
      this.editMode = true;
      this.time = value;
    },
    setTime(value){
      this.editMode = false;
      this.time = value;
    }
  }
};
</script>
<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Edu+NSW+ACT+Foundation:wght@500&family=Lato:wght@300&display=swap");
h1 {
  font-family: "Edu NSW ACT Foundation", cursive;
  font-size: 80px;
  color: rgb(78, 172, 78);
  user-select: none;
}

</style>
