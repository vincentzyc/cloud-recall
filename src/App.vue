<template>
  <div id="app">
    <div class="app-content">
      <router-view/>
      <footer class="flex footer align-middle">
        <div style="width:100%">
          <cube-tab-bar v-model="selectedLabelDefault" :data="tabs" @click="clickHandler"></cube-tab-bar>
        </div>
        <div class="add-recall cubeic-calendar" :class="{active:isActive}" @click="addRecall()"></div>
      </footer>
    </div>
  </div>
</template>
<script>
export default {
  name: "app",
  data() {
    return {
      isActive: false,
      selectedLabelDefault: "",
      tabs: [
        {
          label: "我的回忆",
          icon: "cubeic-home"
        },
        {
          label: "支出统计",
          icon: "cubeic-like"
        }
      ]
    };
  },
  watch: {
    "$route"(n) {
      switch (n.name) {
        case "add":
          this.isActive = true;
          this.selectedLabelDefault = "";
          break;
        case "home":
          this.isActive = false;
          this.selectedLabelDefault = "我的回忆";
          break;
        case "expend":
          this.isActive = false;
          this.selectedLabelDefault = "支出统计";
          break;
      }
    }
  },
  methods: {
    addRecall() {
      this.$router.push("/add");
    },
    clickHandler(label) {
      switch (label) {
        case "我的回忆":
          this.$router.push("/");
          break;
        case "支出统计":
          this.$router.push("/expend");
          break;
      }
    }
  }
  // mounted() {
  // this.$nextTick(function () {
  // window.addEventListener("load", () => {
  //     this.$refs.scroll.refresh();
  // });
  // });
  // }
};
</script>

<style scoped>
.app-content {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  overflow: auto;
  -webkit-overflow-scrolling: touch;
}
.footer {
  position: fixed;
  left: 0;
  bottom: 0;
  width: 100%;
  height: 50px;
  border-top: 1px solid #dedede;
  background: #fff;
  z-index: 99;
}
.add-recall {
  position: absolute;
  bottom: 20px;
  left: 50%;
  width: 52px;
  height: 52px;
  text-align: center;
  line-height: 52px;
  background: #fff;
  border: 1px solid #dedede;
  border-radius: 100%;
  transform: translateX(-50%);
  font-weight: 900;
  color: #666;
  font-size: 27px;
}
.active {
  color: #1e88d7;
}
</style>
