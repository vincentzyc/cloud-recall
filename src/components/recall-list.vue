<template>
  <div class="recall-list">
    <cube-scroll ref="scroll">
      <ul v-for="list in recallList" :key="list.date" class="date-item">
        <h3 class="text-center">{{list.date}}</h3>
        <div class="pd10">
          <li v-for="item in list.items" :key="item.time" class="flex list-item">
            <h4 class="flex-auto">{{item.text}}</h4>
            <span class="mg-r20">￥{{item.amount}}</span>
            <span class>{{item.time}}</span>
          </li>
          <div class="text-center">当日总支出:￥{{list.items.reduce((total, val) => total + parseFloat(val.amount), 0)}}</div>
        </div>
      </ul>
    </cube-scroll>
  </div>
</template>

<script>
export default {
  name: "RecallList",
  data() {
    return {
      recallList: [
        {
          date: "2018-11-11",
          items: [
            {
              text: "午餐",
              time: "12:00-12:30",
              amount: "20"
            },
            {
              text: "看电影",
              time: "19:00-21:00",
              amount: "50"
            }
          ]
        },
        {
          date: "2018-11-12",
          items: [
            {
              text: "早餐",
              time: "7:00-7:30",
              amount: "10"
            },
            {
              text: "公交",
              time: "7:30-8:40",
              amount: "4"
            }
          ]
        },
        {
          date: "2018-11-13",
          items: [
            {
              text: "超市",
              time: "19:00-20:00",
              amount: "150"
            }
          ]
        },
        {
          date: "2018-11-14",
          items: [
            {
              text: "午餐",
              time: "12:00-12:30",
              amount: "20"
            },
            {
              text: "看电影",
              time: "19:00-21:00",
              amount: "50"
            }
          ]
        },
        {
          date: "2018-11-15",
          items: [
            {
              text: "早餐",
              time: "7:00-7:30",
              amount: "10"
            },
            {
              text: "公交",
              time: "7:30-8:40",
              amount: "4"
            }
          ]
        },
        {
          date: "2018-11-16",
          items: [
            {
              text: "超市",
              time: "19:00-20:00",
              amount: "150"
            }
          ]
        },
        {
          date: "2018-11-17",
          items: [
            {
              text: "午餐",
              time: "12:00-12:30",
              amount: "20"
            },
            {
              text: "看电影",
              time: "19:00-21:00",
              amount: "50"
            }
          ]
        },
        {
          date: "2018-11-18",
          items: [
            {
              text: "早餐",
              time: "7:00-7:30",
              amount: "10"
            },
            {
              text: "公交",
              time: "7:30-8:40",
              amount: "4"
            }
          ]
        }
      ]
    };
  },
  methods: {

  },
  mounted() {
    this.$nextTick(function () {
      setTimeout(() => {
        this.$refs.scroll.refresh();
      }, 0);
    });
  },
  created() { }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.recall-list {
  height: calc(100% - 50px);
  padding: 0 10px;
  background: #f2f2f2;
}
.date-item {
  padding: 10px 0;
  background: #ffffff;
  border-radius: 10px;
  margin-top: 10px;
}
.list-item {
  padding: 10px;
  background: #ededed;
  margin-bottom: 10px;
}
.date-item:last-child {
  margin-bottom: 30px;
}
</style>
