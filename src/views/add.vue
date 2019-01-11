<template>
  <div class="add-page">
    <h3 class="text-center fs20 strong">{{formData.date}}</h3>
    <div class="bgfff">
      <ul class="add-wrapper">
        <li v-for="(item,key) in formData.list" :key="key" class="flex row mg-b10">
          <input
            type="text"
            v-model="item.text"
            class="input-text text-center"
            placeholder="事项"
            onfocus="this.classList.add('active')"
            onblur="this.classList.remove('active')"
          >
          <input
            type="number"
            v-model="item.amount"
            class="input-text text-center"
            placeholder="花费"
            onfocus="this.classList.add('active')"
            onblur="this.classList.remove('active')"
          >
          <input
            type="text"
            v-model="item.time"
            class="input-text text-center"
            readonly
            onfocus="this.blur()"
            placeholder="时间"
            @click="showTimeRangePicker(key)"
          >
        </li>
        <div class="text-center pd20 relative fs16">
          <i class="cubeic-remove removeicon" @click="deleteEvent()"></i>
          <span>当日总支出:￥{{allAmount}}</span>
          <i class="cubeic-add addicon" @click="addEvent()"></i>
        </div>
      </ul>
    </div>
    <cube-button :primary="true">保 存</cube-button>
  </div>
</template>
<script>
const dateSegmentData = [
  {
    is: 'cube-date-picker',
    title: '开始时间',
    min: [0, 0],
    max: [23, 59],
    value: new Date(),
    startColumn: 'hour',
    columnCount: 2,
    format: {
      hour: 'hh点', minute: 'mm分'
    },
  },
  {
    is: 'cube-date-picker',
    title: '结束时间',
    min: [0, 0],
    max: [23, 59],
    startColumn: 'hour',
    columnCount: 2,
    format: {
      hour: 'hh点', minute: 'mm分'
    },
  }
]
export default {
  data() {
    return {
      listIndex: "",
      formData: {
        date: this.$util.getFormatDate("yyyy-mm-dd"),
        list: [{
          text: "",
          amount: "",
          time: ""
        }]
      }
    }
  },
  computed: {
    allAmount() {
      return this.formData.list.reduce((total, val) => total + parseFloat(val.amount === "" ? 0 : val.amount), 0);
    }
  },
  methods: {
    addEvent() {
      this.formData.list.push({
        text: "",
        amount: "",
        time: ""
      })
    },
    deleteEvent() {
      this.formData.list.pop()
    },
    showTimeRangePicker(key) {
      this.listIndex = key;
      this.timeRangePicker.show()
    },
    formatTime(arr) {
      let t1 = arr[0][0] < 10 ? "0" + arr[0][0] : arr[0][0];
      let t2 = arr[0][1] < 10 ? "0" + arr[0][1] : arr[0][1];
      let t3 = arr[1][0] < 10 ? "0" + arr[1][0] : arr[1][0];
      let t4 = arr[1][1] < 10 ? "0" + arr[1][1] : arr[1][1];
      return `${t1}:${t2}-${t3}:${t4}`;
    }
  },
  mounted() {
    this.$nextTick(() => {
      this.timeRangePicker = this.$createSegmentPicker({
        data: dateSegmentData,
        onSelect: (selectedDates, selectedVals, selectedTexts) => {
          this.formData.list[this.listIndex].time = this.formatTime(selectedVals);
        },
        onNext: (i, selectedDate, selectedValue, selectedText) => {
          dateSegmentData[1].min = selectedDate
          this.timeRangePicker.$updateProps({
            data: dateSegmentData
          })
        }
      })
    })
  }
}
</script>
<style lang="stylus" scoped>
.add-page {
  padding: 10px;
  margin-bottom: 50px;
  background: #f2f2f2;

  .add-wrapper {
    margin: 15px 0;
  }

  .input-text {
    width: 33.3333%;
    transition: 0.3s;
    padding: 10px 0;
    border: 1px solid #eee;
  }

  .input-text.active {
    width: 100%;
  }

  .addicon {
    position: absolute;
    right: 15px;
    top: 5px;
    color: #666;
    font-size: 24px;
    padding: 10px;
  }

  .removeicon {
    position: absolute;
    left: 15px;
    top: 5px;
    color: #666;
    font-size: 24px;
    padding: 10px;
  }
}
</style>


