<template>
  <div id="app" class="container">
<!-- :key должен быть уникальным id элемента, как только понадобится удалить какой то из элементов
  все поплывет потому сто нет конкретного указателя. иначе countStopWatches должен быть массивом как минимум,
  и надо использовать idx в качестве указателя v-for="(item, idx) in countStopwatches" :key="idx"-->
    <StopWatch v-for="item in countStopwatches" :key="item"/>
<!--на мой взгяд компонент - лишний, и вешать событие клика на копонент это неправильно, компаоненты события генерят.
поэтому раз уж так, то слушатель внутри, эмит события add наружу и здесь уже on add -->
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
