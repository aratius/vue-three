<template>
  <div id="url-table">
    <table>
      <tr>
        <td id="head">{{ when }} period : ( {{ startTime }} ~ )</td>
      </tr>
      <tr>
        <td>
          URL :
          <input type="url" v-model="url" />
        </td>
        <td>
          <button @click="url = ''">clear</button>
        </td>
      </tr>
      <tr>
        <td>
          TIME :
          <input type="time" v-model="time" />
        </td>
        <td>
          <button @click="time = ''">clear</button>
        </td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  name: "inUrl",
  props: {
    when: Object, //what number og period
    startTime: String, //start time of period (not set time)
    setDate: Object, //set date for all
    getUrl: Object, //get previous url from localStorage
    getTime: Object //get previous time from localStorage
  },
  data: function() {
    return {
      url: "", //this url
      time: "", //this time
      flag: 0 //flag for run three times
    };
  },
  methods: {
    //get now time format for compare
    getDateTime() {
      let today = new Date();
      let year = today.getFullYear();
      let month = today.getMonth() + 1;
      let date = today.getDate();
      let hour = today.getHours();
      let minute = today.getMinutes();

      month = ("000" + month).slice(-2);
      date = ("000" + date).slice(-2);
      hour = ("000" + hour).slice(-2);
      minute = ("000" + minute).slice(-2);
      let now =
        "" + year + "-" + month + "-" + date + "-" + hour + "-" + minute;
      //format : 2000-11-29-05-11
      return now;
    },

    //exchange time from 00:00 to 00-00 (like this)
    exchangeTime() {
      let sep = this.time.split(":");
      return sep[0] + "-" + sep[1];
    },

    // join class methods
    joinClass() {
      console.log(this.url);
      window.open(
        this.url,
        "_blank",
        "menubar=0,width=300,height=200,top=100,left=100"
      );
    }
  },
  mounted() {
    //set localStorage val that's given by parent
    this.url = this.getUrl[this.when - 1];
    this.time = this.getTime[this.when - 1];

    //join url or not (main function)
    setInterval(
      function() {
        //1. get now time
        let now = this.getDateTime();
        // console.log(now);

        //2. get set time
        let setTime = "" + this.setDate + "-" + this.exchangeTime();

        //3 compare  ブラウザのzoomはたまに一発で入れないので一応2回通しておく
        if (now == setTime && this.time != "00:00" && this.flag < 3) {
          console.log("hi");
          this.joinClass();
          this.flag++;
        } else if (now == setTime && this.flag == 3) {
          this.time = "";
          this.flag = 0;
        }
      }.bind(this),
      10000
    );
  },
  watch: {
    //save its val in its parent ($emit)
    url: function(val) {
      this.$emit("submit-url", val, this.when);
    },
    time: function(val) {
      this.$emit("submit-time", val, this.when);
    }
  }
};
</script>

<style scoped>
#url-table {
  display: flex;
  align-items: center;
  text-align: left;
  margin: 4px;
  padding: 4px;
  border: 1px solid #2c3e50;
  border-radius: 7px;
  background-color: rgba(255, 255, 255, 0.7);
}

#head {
  font-weight: bold;
}
</style>
