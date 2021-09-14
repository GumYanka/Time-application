<template>
  <div id="app">
    <h1 class="title">World time application</h1>

    <zones @update-time="updateTime" @add-time="addTime" />

    <h1 v-for="(time, index) in times.slice(0, 5)" :key="index" class="title">
      {{ time.hours }}:{{ time.minutes }}:{{ time.seconds }} -
      {{ time.details.timezone }}
      <button @click="deleteItem(index)" class="btn default-el ml-1" >
        delete
      </button>
    </h1>
    <div v-if="times.length > 5" class="title text">
  This is the maximum number of zones that can be viewed.
</div>
<!-- <span v-else-if="time === time.details.timezone" class="title text">
  This zone already exists.
</span> -->

  </div>
</template>

<script>
import Zones from "./components/Zones.vue";
import timeDetails from "@/mixins/timeDetails.js";

export default {
  mixins: [timeDetails],
  name: "App",
  components: {
    Zones,
  },
  data() {
    return {
      times: [],
      zone: "Europe/Kiev",
    };
  },
  mounted() {
    this.getTimeDetails().then((timeDetails) => {
      this.addTime(timeDetails);
    });
  },
  methods: {
    updateTime(timeDetails) {
      if (!this.times.length) {
        this.addTime(timeDetails);
        return;
      }

      this.times.splice(this.times.length - 1, 1, timeDetails);
    },
    addTime(time) {
      this.times.push(time);
    },
    deleteItem(index) {
      this.times.splice(index, 1);
},
say: function (message) {
      alert(message)
    }
},
computed:{
}
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}

.title {
  text-align: center;
}

.text{
  font-weight: 600;
}

.default-el {
  border: 1px solid #75c5b7;
  padding: 10px;
  cursor: pointer;
  outline: none;
  transition: all 0.2s;
  font-weight: 600;
  border-radius: 2px;
  color: #75c5b7;
  background: #f8fff6;
}

.btn {
  background-color: #75c5b7;
  color: #fff;

  &:active {
    background-color: #fff;
  }
}

.ml-1 {
  margin-left: 0.2rem;
}
</style>
