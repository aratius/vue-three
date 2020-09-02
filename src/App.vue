<template>
  <div id="app">
    <Three />
  </div>
</template>

<script>
import Three from "./components/Three";

export default {
  name: "app",
  components: {
    Three
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  display: flex;
  flex-direction: column;
  align-items: center;
  color: #2c3e50;
  padding-top: 10px;
  /* position: relative; */
  user-select: none; /* CSS3 */
  -moz-user-select: none; /* Firefox */
  -webkit-user-select: none; /* Safari、Chromeなど */
  -ms-user-select: none; /* IE10かららしい */
}

#date {
  margin-bottom: 5px;
}

#button-help {
  width: 80px;
  height: 40px;
  font-size: large;
  position: absolute;
  right: 15px;
  bottom: 10px;
  border-radius: 5px;
}

.help-enter-active,
.help-leave-active {
  transition: opacity 0.3s;
  opacity: 0;
}

.help-enter,
.help-leave-to {
  opacity: 0;
}

.help-leave,
.help-enter-to {
  opacity: 1;
}
</style>