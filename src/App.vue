<template>
  <div id="app">
    <h1>Automatic zoom attender</h1>
    <input type="date" v-model="setDate" id="date" />
    <InUrl
      :when="1"
      startTime="09:10"
      :setDate="setDate"
      :getUrl="url"
      :getTime="time"
      @submit-url="subUrl"
      @submit-time="subTime"
    ></InUrl>
    <InUrl
      :when="2"
      startTime="10:50"
      :setDate="setDate"
      :getUrl="url"
      :getTime="time"
      @submit-url="subUrl"
      @submit-time="subTime"
    ></InUrl>
    <InUrl
      :when="3"
      startTime="13:20"
      :setDate="setDate"
      :getUrl="url"
      :getTime="time"
      @submit-url="subUrl"
      @submit-time="subTime"
    ></InUrl>
    <InUrl
      :when="4"
      startTime="15:00"
      :setDate="setDate"
      :getUrl="url"
      :getTime="time"
      @submit-url="subUrl"
      @submit-time="subTime"
    ></InUrl>
    <InUrl
      :when="5"
      startTime="16:40"
      :setDate="setDate"
      :getUrl="url"
      :getTime="time"
      @submit-url="subUrl"
      @submit-time="subTime"
    ></InUrl>
    <transition name="help">
      <Help v-show="showHelp" @close="buttonAction" />
    </transition>
    <button @click="buttonAction" id="button-help">{{ buttonMsg }}</button>
    <rotate-box></rotate-box>
  </div>
</template>

<script>
import RotateBox from "./components/RotateBox";
import InUrl from "./components/InUrl.vue";
import Help from "./components/Help.vue";

export default {
  name: "app",
  components: {
    RotateBox,
    InUrl,
    Help
  },
  data: function() {
    return {
      when: {}, //period for props
      setDate: { p1: "2000-11-29" },
      url: ["", "", "", "", ""], //url for props n' emit
      time: ["", "", "", "", ""], //time for props n' emit
      showHelp: false,
      buttonMsg: "help"
    };
  },
  methods: {
    getToday() {
      let today = new Date();
      let year = today.getFullYear();
      let month = today.getMonth() + 1;
      let date = today.getDate();

      month = ("000" + month).slice(-2);
      date = ("000" + date).slice(-2);
      let now = "" + year + "-" + month + "-" + date;
      return now;
    },
    subUrl(val, num) {
      this.url[num - 1] = val;
      let keyU = num - 1 + "U";
      localStorage.setItem(keyU, val);
    },
    subTime(val, num) {
      this.time[num - 1] = val;
      let keyT = num - 1 + "T";
      localStorage.setItem(keyT, val);
    },
    buttonAction() {
      this.showHelp = !this.showHelp;
      this.showHelp ? (this.buttonMsg = "close") : (this.buttonMsg = "help");
    }
  },
  created() {
    //*
    this.setDate = this.getToday();
    localStorage.getItem("setDate")
      ? (this.setDate = localStorage.getItem("setDate"))
      : (this.setDate = this.getToday());
    for (let i = 0; i < this.url.length; i++) {
      let keyU = i + "U";
      let keyT = i + "T";
      localStorage.getItem(keyU) && localStorage.getItem(keyU) != "undefined"
        ? (this.url[i] = localStorage.getItem(keyU))
        : (this.url[i] = "");
      localStorage.getItem(keyT) && localStorage.getItem(keyT) != "undefined"
        ? (this.time[i] = localStorage.getItem(keyT))
        : (this.time[i] = "");
    }
  },
  watch: {
    setDate: function(val) {
      localStorage.setItem("setDate", val);
    }
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