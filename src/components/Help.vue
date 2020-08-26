<template>
  <div>
    <div id="help">
      <div id="titles">
        <div class="title" id="titleL" @click="show = true">
          <h1>How to set class</h1>
        </div>
        <div class="title" id="titleR" @click="show = false">
          <h1>Required settings</h1>
        </div>
      </div>
      <div id="contents-area">
        <Set v-if="show" />
        <Req v-if="!show" />
      </div>
    </div>
    <div id="cancel" @click="close">×</div>
  </div>
</template>

<script>
import Set from "./HelpSet.vue";
import Req from "./HelpReq.vue";

export default {
  data: function() {
    return {
      show: true
    };
  },
  components: {
    Set,
    Req
  },
  methods: {
    close() {
      this.$emit("close");
    }
  }
};
</script>

<style scoped>
#help {
  width: 80vw;
  height: 80vh;
  margin: auto;
  padding-bottom: 5px;
  background-color: rgba(240, 240, 240, 0.9);
  position: absolute;
  top: 10vh;
  left: 10vw;
  border-radius: 5vw;
  opacity: 1;
  box-shadow: 0 5px 10px 10px rgb(0, 0, 0, 0.2);
  overflow: hidden;
}

#titles {
  width: 100%;
  display: flex;
  font-size: 10px;
  border-bottom: 1px solid rgb(182, 182, 182);
}

.title {
  width: 50%;
  text-align: center;
}

#titleL {
  border-right: 1px solid rgb(182, 182, 182);
}

#titleR:hover {
  border-top-right-radius: 5vw;
  background-color: rgb(211, 211, 211);
}

#titleL:hover {
  border-top-left-radius: 5vw;
  background-color: rgb(211, 211, 211);
}

#contents-area {
  width: 70%;
  height: 90%;
  margin: auto;
  /* background-color: rgb(228, 228, 228); */
  overflow-x: hidden;
}

#cancel {
  width: 40px;
  height: 40px;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 40px;
  position: absolute;
  top: 8%;
  right: 8%;
  background-color: rgb(236, 236, 236);
  border-radius: 20px;
  box-shadow: 0 3px 5px 5px rgba(0, 0, 0, 0.05);
}

#cancel:hover {
  background-color: rgb(224, 224, 224);
}
</style>
