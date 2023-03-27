<template>
    <div class="AddButton">
      <button @click="addStopwatch">+</button>
    </div>
</template>
  
<script>
export default {
    methods: {
      addStopwatch() {
        const stopwatch = {
          id: Date.now(), // уникальный id для v-for
          time: 0,
          isRunning: false,
          intervalId: null
        };
        this.$emit("stopwatchAdded", stopwatch);
      }
    }
};
</script>
<style scoped>
.AddButton {
  display: flex;
  flex-direction: column;
  align-items: center; 
  margin: 55px;
  padding: 20px;
  background-color: #696969;
  width: 350px;
  height: 200px;
  box-sizing: border-box;
}

button {
  background-color: #696969;
  border: none;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 5rem;
  height: 100%;
  width: 100%;
  color: #9E9E9E;
  transition: all 0.3s ease;
}

button:hover {
  background-color: #696969;
  color: #cecece;
  cursor: pointer;
}

/* стили для устройств с шириной экрана 320px и больше */
@media only screen and (min-width: 320px) {
  .AddButton {
    flex-direction: column;
  }

  .AddButton {
    margin: 20px;
    margin-top: 50px;
    width: 90%;
    height: 200px;
  }

}

/* стили для устройств с шириной экрана 768px и больше */
@media only screen and (min-width: 768px) {
  .AddButton {
    flex-direction: row;
    flex-wrap: wrap;
  }

  .AddButton {
    margin: 26px;
    margin-top: 50px;
    width: 43%;
    height: 200px;
  }
}

/* стили для устройств с шириной экрана 1024px и больше */
@media only screen and (min-width: 1024px) {
  .AddButton {
    margin: 20px;
    margin-top: 50px;
    width: 30%;
    height: 200px;
  }
}
</style>