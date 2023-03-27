<template>
  <div class="stopwatch">
    <div class="time">
      {{ hours }} <span v-show="hours">:</span> {{ minutes }}
      <span v-show="minutes || hours">:</span> {{ seconds }}
    </div>
    <div class="btn-block">
      <div v-on:click="start" v-show="!isActive && isStopped">
        <img src="img/start.png" alt="start" />
      </div>

      <div v-on:click="stop" v-show="isActive">
        <img src="img/pause.png" alt="stop" class="stop" />
      </div>

      <div v-on:click="reset">
        <img src="img/stop.png" alt="reset" class="reset"  />
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

      let activeTimer = document.querySelector(".stopwatch");
      let activeBorder = document.querySelector(".time");

      if (this.isActive == true) {
        activeTimer.classList.add("active");
        activeBorder.classList.add("active-border");
       document.querySelectorAll(".reset").src="img/active-stop.png";
       document.querySelectorAll(".stop").src="img/active-pause.png";
      }
       
    },
    stop() {
      clearInterval(this.interval);
      this.interval = null;
      this.isStopped = true;
      this.isActive = false;

      let activeTimer = document.querySelector(".stopwatch");
      let activeBorder = document.querySelector(".time");


      if (this.isActive != true) {
        activeTimer.classList.remove("active");
        activeBorder.classList.remove("active-border");
        document.querySelectorAll(".reset").src="img/stop.png";
        document.querySelectorAll(".stop").src="img/pause.png";
      }
    },
    reset() {
      clearInterval(this.interval);
      this.interval = null;
      (this.hours = ""), (this.minutes = "");
      this.seconds = 0;
    },
  },
};
</script>
