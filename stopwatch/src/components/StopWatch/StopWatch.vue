<template>
  <div class="stopwatch" :class="{ 'active': isActive }">
    <div class="time" :class="{ 'active-border': isActive }">
      <!-- {{ hours }} <span v-show="hours">:</span> {{ minutes }} -->
      <!-- <span v-show="minutes || hours">:</span> {{ seconds }} -->
      {{ formatTime }}
    </div>
    <div class="btn-block">
<!--      желательно использовать v-if а еще лучше вообще не использовать отдельный элемент, просто менять иконку,
и по клику менять стейт isStopped и прочее типа того из за v-show еще промаргивание есть-->
      <div v-on:click="startStop">
        <img :src="isActive ? 'img/active-pause.png' : 'img/start.png'" alt="start" />
      </div>
<!--      <div v-on:click="start" v-show="!isActive">-->
<!--        <img src="img/start.png" alt="start" />-->
<!--      </div>-->

<!--      <div v-on:click="stop" v-show="isActive">-->
<!--        <img src="img/active-pause.png" alt="stop" class="stop" v-if="isActive" />-->
<!--        <img src="img/pause.png" alt="stop" class="stop" v-else />-->
<!--      </div>-->
      <div v-on:click="reset">
        <img :src="isActive ? 'img/active-stop.png' : 'img/stop.png'" alt="start" />
      </div>
<!--      <div v-on:click="reset">-->
<!--        <img src="img/active-stop.png" alt="reset" class="reset" v-if="isActive" />-->
<!--        <img src="img/stop.png" alt="reset" class="reset" v-else />-->
<!--      </div>-->
    </div>
  </div>
</template>

<script>
import "./StopWatch.css";

export default {
  data() {
    return {
      // hours: "",
      // minutes: "",
      // seconds: 0,
      // interval: null,
      startTime: null,
      elapsedTime: 0,
      isRunning: false,
      isActive: false,
      isStopped: true,
    };
  },
  computed: {
    formatTime() {
      let seconds = Math.floor(this.elapsedTime / 1000) % 60;
      let minutes = Math.floor(this.elapsedTime / 1000 / 60) % 60;
      let hours = Math.floor(this.elapsedTime / 1000 / 60 / 60);

      return `${this.pad(hours)}:${this.pad(minutes)}:${this.pad(seconds)}`;
    },
  },
  methods: {      // в код не лез, на мой взгляд слишком сложно, надо было использовать что то вроде moment.js и работать с объектом даты
    startStop() {
      this.isActive ? this.stop() : this.start()
    },
    start() {
      // if (this.interval) return;
      // this.interval = setInterval(() => {
      //   this.seconds++;
      //   if (this.seconds >= 60) {
      //     this.seconds = 0;
      //     this.minutes++;
      //   }
      //   if (this.minutes >= 60) {
      //     this.seconds = 0;
      //     this.minutes = 0;
      //     this.hours++;
      //   }
      // }, 1000);

      this.startTime = performance.now() - this.elapsedTime;
      this.isRunning = true;
      requestAnimationFrame(this.tick);

      this.isActive = true;
      this.isStopped = false;
      this.isRunning = true;
    },
    stop() {
      // clearInterval(this.interval);
      // this.interval = null;
      this.isRunning = false;
      this.isStopped = true;
      this.isActive = false;
    },
    reset() {
      // clearInterval(this.interval);
      // this.interval = null;
      // (this.hours = ""), (this.minutes = "");
      // this.seconds = 0;
      this.elapsedTime = 0;
      this.isRunning = false;
      this.isStopped = true;
      this.isActive = false;
    },
    tick(timestamp) {
      if (!this.isRunning) return;
      this.elapsedTime = timestamp - this.startTime;
      requestAnimationFrame(this.tick);
    },
    pad(num, size = 2) {
      let s = num + "";
      while (s.length < size) s = "0" + s;
      return s;
    },
  },
};
</script>
