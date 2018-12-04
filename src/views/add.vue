<template>
  <div class="add-page">
    <h3 class="text-center fs20 strong">{{formData.date}}</h3>
    <div class="bgfff">
      <ul class="add-wrapper">
        <li v-for="(item,key) in formData.list" :key="key" class="flex row">
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
            onfocus="this.classList.add('active')"
            onblur="this.classList.remove('active')"
            placeholder="时间"
            @click="showTimeRangePicker(key)"
          >
        </li>
        <div class="text-center pd20">当日总支出:￥{{allAmount}}</div>
      </ul>
      <!-- <li v-for="item in list.items" :key="item.time" class="flex list-item">
          <h4 class="flex-auto">{{item.text}}</h4>
          <span class="mg-r20">￥{{item.amount}}</span>
          <span class>{{item.time}}</span>
      </li>-->
    </div>
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
        date: this.$api.getFormatDate("yyyy-mm-dd"),
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
      let total = this.formData.list.reduce((total, val) => total + parseFloat(val.amount), 0);
      return total ? total : 0;
    }
  },
  methods: {
    showTimeRangePicker(key) {
      this.listIndex = key;
      this.timeRangePicker.show()
    }
  },
  mounted() {
    this.$nextTick(() => {
      this.timeRangePicker = this.$createSegmentPicker({
        data: dateSegmentData,
        onSelect: (selectedDates, selectedVals, selectedTexts) => {
          this.formData.list[this.listIndex].time = selectedVals;
          // this.$createDialog({
          //   type: 'warn',
          //   content: `Selected Items: <br/> - 开始时间: ${selectedTexts[0].join('')} <br/> - 结束时间: ${selectedTexts[1].join('')}`,
          //   icon: 'cubeic-alert'
          // }).show()
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
}
</style>


