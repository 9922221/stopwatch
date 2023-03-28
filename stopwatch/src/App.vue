<template>
  <div id="app" class="container">
    <StopWatch v-for="item in countStopwatches" :key="item"/>

    <AddStopWatch v-on:click="add" />

  </div>
</template>

<script>
import "./main.css";
import StopWatch from "./components/StopWatch/StopWatch.vue";
import AddStopWatch from "./components/AddStopWatch/AddStopWatch.vue";

export default {
  name: "App",
  components: {
    StopWatch,
    AddStopWatch
  },
  data: () => ({
    countStopwatches: 4
  }),

  methods: {
    add() {
      this.countStopwatches++
    },
  }
}
</script>
