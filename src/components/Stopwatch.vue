<template>
    <div class="stopwatch">
      <div class="time" :class="{active: isActive}">{{ formattedTime }}</div>
      <hr class="line" :class="{active: isActive}">
      <div class="controls">
        <button
            :class="{active: isActive}"
            @click="startStopwatch()" 
            v-if="!localStopwatch.isRunning"
        >
        ▶
        </button>
        <button
            :class="{active: isActive}"
            class="pause" 
            @click="pauseStopwatch()" 
            v-if="localStopwatch.isRunning"
        >
        ||
        </button>
        <button
            :class="{active: isActive}"
            class="reset" 
            @click="resetStopwatch()" 
            :disabled="localStopwatch.time === 0"
        >
        ■
        </button>
      </div>
    </div>
  </template>
  
<script>
export default {
    props: {
      stopwatch: {
        type: Object,
        required: true
      }
    },
    data() {
      return {
        localStopwatch: { ...this.stopwatch },
        isActive: false
      };
    },
    computed: {
        formattedTime() {
            const hours = Math.floor(this.localStopwatch.time / 3600); // делим время секундомера на 3600 (количество секунд в часе). Это позволяет получить количество часов в оставшемся времени.
            const minutes = Math.floor((this.localStopwatch.time % 3600) / 60);
            const seconds = Math.floor(this.localStopwatch.time % 60);

            const formattedHours = hours.toString().padStart(2, "0"); // ограничиваем числа до 2 в таймере
            const formattedMinutes = minutes.toString().padStart(2, "0");
            const formattedSeconds = seconds.toString().padStart(2, "0");

            if (hours > 0) { // формат вывода
                return `${formattedHours}:${formattedMinutes}:${formattedSeconds}`;
            } else if (minutes > 0) {
                return `${formattedMinutes}:${formattedSeconds}`;
            } else {
                return `${formattedSeconds}`;
            }
        }
    },
    methods: {
        startStopwatch() { // запуск таймера
            this.localStopwatch.isRunning = true;
            this.localStopwatch.intervalId = setInterval(() => {
                this.localStopwatch.time++;
            }, 1000); // Уменьшите это значение, чтобы увидеть часы)
            this.isActive = true;
        },
        pauseStopwatch() { // пауза
            this.localStopwatch.isRunning = false;
            clearInterval(this.localStopwatch.intervalId);
            this.isActive = false;
        },
        resetStopwatch() { // остановка
            this.localStopwatch.time = 0;
            this.localStopwatch.isRunning = false;
            clearInterval(this.localStopwatch.intervalId);
            this.isActive = false;
        }
    }
};
</script>

<style scoped>
.stopwatch {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin: 55px;
    padding: 20px;
    background-color: #696969;
    width: 350px;
    height: 200px;
    box-sizing: border-box;
    overflow: hidden;
}

.time {
    display: flex;
    justify-content: center;
    align-items: center;
    font-family: 'Gotham Pro';
    font-size: 3rem;
    font-weight: 700;
    width: 300px;
    height: 100px;
    color: #9E9E9E;
    border-radius: 8px;
    margin-bottom: 20px;
}

.time.active {
    color: #ffffff;
}

.controls {
    display: flex;
    justify-content: center;
    align-items: center;
}

.reset {
    font-size: 4.7rem;
    margin-bottom: 10px;
}

.pause {
    font-weight: 900;
    margin-bottom: 8px;
}
  
.line {
    box-sizing: border-box;
    border: none;
    border-top: 3px #9e9e9e solid;
    width: 113%;
    size: 10px;
    margin: 0;
    padding: 0;
}

.line.active {
    color: #ffffff;
    border-top: 3px #ffffff solid;
}

button {
    font-size: 3rem;
    border: none;
    transition: all 0.3s ease;
    background-color: #696969;
    color: #9e9e9e;
    width: 150px;
    display: inline-block;
}

button.active {
    color: #ffffff;
}

button:hover {
    background-color: #696969;
    color: #cecece;
    cursor: pointer;
}

button:disabled {
    opacity: 0.5;
    cursor: not-allowed;
}

/* стили для устройств с шириной экрана 320px и больше */
@media only screen and (min-width: 320px) {
  .line {
    width: 200%;
  }

  .stopwatch {
    margin: 20px;
    margin-top: 50px;
    width: 90%;
    height: 200px;
    overflow: hidden;
  }

}

/* стили для устройств с шириной экрана 768px и больше */
@media only screen and (min-width: 768px) {
  .stopwatch {
    margin: 26px;
    margin-top: 50px;
    width: 43%;
    height: 200px;
    overflow: hidden;
  }

  .line {
    width: 200%;
  }

}

/* стили для устройств с шириной экрана 1024px и больше */
@media only screen and (min-width: 1024px) {
  .stopwatch {
    margin: 20px;
    margin-top: 50px;
    width: 30%;
    height: 200px;
    overflow: hidden;
  }

  .line {
    width: 200%;
  }

}

</style>