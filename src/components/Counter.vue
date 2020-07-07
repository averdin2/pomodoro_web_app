<template>
  <div>
    <!-- Overlay -->
    <div
      class="overlay"
      v-bind:class="{ 'blue-bg': isStart, 'green-bg': isBreak, 'red-bg': isStop }"
    ></div>
    <div class="counter-container">
      <!-- Header -->
      <h1
        class="header"
        v-bind:class="{ 'blue-color': isStart, 'green-color': isBreak, 'red-color': isStop }"
      >Pomodoro Timer</h1>
      <!-- Timer -->
      <div
        class="timer"
        v-bind:class="{ 'blue-color': isStart, 'green-color': isBreak, 'red-color': isStop }"
      >{{ displayMinutes }}:{{ displaySeconds }}</div>

      <div>
        <!-- Start Button -->
        <button
          class="btn start-btn"
          v-bind:class="{'not-active': (isStart || !phase)}"
          v-on:click="changeState(0), timer(timeLength)"
        >Start Timer</button>
        <!-- Break Start Button -->
        <button
          class="btn break-btn"
          v-bind:class="{'not-active': (isBreak || phase)}"
          v-on:click="changeState(1), displayTime(timeInSeconds(breakLength)), timer(breakLength)"
        >Start Break</button>
        <!-- Reset Button -->
        <button
          class="btn reset-btn"
          v-on:click="changeState(3), displayTime(timeInSeconds(timeLength))"
        >Reset</button>
      </div>
    </div>
  </div>
</template>

<script>
// I am deciding to make this initial approach non modular meaning that values for the timer
// length and break length are predetermined. Some code may be commented out to reflect this.
// The plan is to then come back once minimum functionality is completed to make functions more
// modular and add functionality to specify time of the timer.

export default {
  props: ["time"],
  data: () => ({
    // Time to be displayed
    displayMinutes: 0,
    displaySeconds: 0,
    // Length of timer and break
    timeLength: 25,
    breakLength: 5,
    // I want to note here that using three values is not very modular,
    // but for time's sake I decided to stick with this implementation.
    isStart: false,
    isBreak: false,
    isStop: false,
    isReset: false,
    // Horrible phase variable
    phase: true
  }),
  // computed: {
  //   timeInSeconds() {
  //     return this.time * 60;
  //   }
  // },
  mounted() {
    this.displayTime(this.timeInSeconds(this.timeLength));
  },
  methods: {
    // Method that computes given time value from minutes to seconds
    timeInSeconds(time) {
      return time * 60;
    },
    // Method to calculate minutes and seconds and display the time for the coutner
    displayTime(t) {
      const minutes = Math.floor(t / 60);
      const seconds = t % 60;

      this.displayMinutes = minutes < 10 ? "0" + minutes : minutes;
      this.displaySeconds = seconds < 10 ? "0" + seconds : seconds;
    },
    // Method that counts down based on a given time passed in
    timer(time) {
      let timeLeft = this.timeInSeconds(time);

      const interval = setInterval(() => {
        timeLeft = timeLeft - 1;

        if (this.isReset === true) {
          clearInterval(interval);
          return;
        }

        if (timeLeft < 0) {
          this.changeState(2);
          this.phase = !this.phase;
          clearInterval(interval);
          return;
        }

        this.displayTime(timeLeft);
      }, 1000);
    },

    // Methods for changing color values
    changeState(value) {
      switch (value) {
        case 0:
          this.isStart = true;
          this.isBreak = false;
          this.isStop = false;
          this.isReset = false;
          break;
        case 1:
          this.isStart = false;
          this.isBreak = true;
          this.isStop = false;
          this.isReset = false;
          break;
        case 2:
          this.isStart = false;
          this.isBreak = false;
          this.isStop = true;
          this.isReset = false;
          break;
        case 3:
          this.isStart = false;
          this.isBreak = false;
          this.isStop = false;
          this.isReset = true;
          this.phase = true;
          break;
      }
    }
  }
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=MuseoModerno:wght@500&display=swap");

body {
  font-family: "MuseoModerno", cursive;
}

.overlay {
  position: absolute;
  top: 0;
  left: 0;
  z-index: -1;
  height: 100vh;
  width: 100vw;
}

.counter-container {
  display: flex;
  flex-direction: column;
  height: 30vh;
  justify-content: space-between;
  align-items: center;
}

.header {
  font-size: 2.3rem;
}

.timer {
  font-size: 2rem;
}

/* Color style classes */

/* BLUE */
.blue-bg {
  background-color: lightblue;
}

.blue-color {
  color: dodgerblue;
}

/* GREEN */
.green-bg {
  background-color: palegreen;
}

.green-color {
  color: mediumseagreen;
}

/* RED */
.red-bg {
  background-color: lightsalmon;
}

.red-color {
  color: indianred;
}

/* Button styles */
.btn {
  border: 1.5px solid black;
  border-radius: 10px;
  padding: 10px 20px;
  margin: 0 5px;
  background-color: transparent;
  transition: color 0.5s ease, border 0.5s ease;
  font-family: "MuseoModerno", cursive;
  font-size: 1rem;
  cursor: pointer;
}

.not-active {
  display: none;
}

.btn:hover,
.btn:focus {
  outline: none;
}

/* Button color styles */
.start-btn {
  border: 1.5px solid dodgerblue;
  color: dodgerblue;
}

.start-btn:hover,
.start-btn:focus {
  border: 1.5px solid royalblue;
  color: royalblue;
}

.break-btn {
  border: 1.5px solid mediumseagreen;
  color: mediumseagreen;
}

.break-btn:hover,
.break-btn:focus {
  border: 1.5px solid seagreen;
  color: seagreen;
}

.reset-btn {
  border: 1.5px solid indianred;
  color: indianred;
}

.reset-btn:hover,
.reset-btn:focus {
  border: 1.5px solid crimson;
  color: crimson;
}
</style>