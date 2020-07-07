<template>
  <div id="app">
    <Counter />
    <!-- <Counter :time="10" /> -->
  </div>
</template>

<script>
import Counter from "./components/Counter.vue";

export default {
  name: "App",
  components: {
    Counter
  }
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
#app {
  display: flex;
  height: 100vh;
  justify-content: center;
  align-items: center;
}
</style>
