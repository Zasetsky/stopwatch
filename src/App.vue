<template>
  <div class="app">
    <div class="stopwatches">
      <stopwatch v-for="stopwatch in stopwatches" :key="stopwatch.id" :stopwatch="stopwatch" />
      <add-button @stopwatchAdded="addStopwatch" />
    </div>
  </div>
</template>

<script>
import Stopwatch from "./components/Stopwatch.vue";
import AddButton from "./components/AddButton.vue";

export default {
  components: {
    Stopwatch,
    AddButton
  },
  data() {
    return {
      stopwatches: [], // список секундомеров
    };
  },
  methods: {
    addStopwatch(stopwatch) { 
      this.stopwatches.push(stopwatch);
    }
  }
};
</script>

<style >
body {
  margin: 0;
  background-color: #353638;
}

.stopwatches {
  display: flex;
  flex-wrap: wrap;
}

</style>
