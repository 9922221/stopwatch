<template>
  <div class="stopwatch" :class="{ 'active': isActive }">
    <div class="time" :class="{ 'active-border': isActive }">
      {{ hours }} <span v-show="hours">:</span> {{ minutes }}
      <span v-show="minutes || hours">:</span> {{ seconds }}
    </div>
    <div class="btn-block">
      <div v-on:click="start" v-show="!isActive && isStopped">
        <img src="img/start.png" alt="start" />
      </div>

      <div v-on:click="stop" v-show="isActive">
        <img src="img/active-pause.png" alt="stop" class="stop" v-if="isActive" />
        <img src="img/pause.png" alt="stop" class="stop" v-else />
      </div>

      <div v-on:click="reset">
        <img src="img/active-stop.png" alt="reset" class="reset" v-if="isActive" />
        <img src="img/stop.png" alt="reset" class="reset" v-else />
      </div>
    </div>
  </div>
</template>

<script>
import "./StopWatch.css";

export default {
  data() {
    return {
      hours: "",
      minutes: "",
      seconds: 0,
      interval: null,
      isRunning: false,
      isActive: false,
      isStopped: true,
    };
  },
  methods: {
    start() {
      if (this.interval) return;
      this.interval = setInterval(() => {
        this.seconds++;
        if (this.seconds >= 60) {
          this.seconds = 0;
          this.minutes++;
        }
        if (this.minutes >= 60) {
          this.seconds = 0;
          this.minutes = 0;
          this.hours++;
        }
      }, 1000);
      this.isActive = true;
      this.isStopped = false;
      this.isRunning = true;
    },
    stop() {
      clearInterval(this.interval);
      this.interval = null;
      this.isStopped = true;
      this.isActive = false;
    },
    reset() {
      clearInterval(this.interval);
      this.interval = null;
      (this.hours = ""), (this.minutes = "");
      this.seconds = 0;
      this.isStopped = true;
      this.isActive = false;
    },
  },
  props: ["id"],
};
</script>
