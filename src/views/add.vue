<template>
  <div class="add-page">
    <h3 class="text-center fs20 strong">{{formData.date}}</h3>
    <div class="bgfff">
      <ul class="flex add-wrapper">
        <li class="flex-auto input-text">
          <input type="text" class="text-center col-12" placeholder="事项">
        </li>
        <li>
          <input type="number" class="text-center col-12" placeholder="花费">
        </li>
        <li @click="showTimeRangePicker">
          <input type="text" class="text-center col-12" readonly onfocus="this.blur()" placeholder="时间">
        </li>
      </ul>
      <!-- <li v-for="item in list.items" :key="item.time" class="flex list-item">
          <h4 class="flex-auto">{{item.text}}</h4>
          <span class="mg-r20">￥{{item.amount}}</span>
          <span class>{{item.time}}</span>
      </li>-->
      <!-- <div class="text-center">当日总支出:￥{{listItems.reduce((total, val) => total + parseFloat(val.amount), 0)}}</div> -->
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
      formData: {
        date: this.$api.getFormatDate("yyyy-mm-dd"),
        listItems: []
      }
    }
  },
  methods: {
    showTimeRangePicker() {
      this.timeRangePicker.show()
    }
  },
  mounted() {
    this.$nextTick(() => {
      this.timeRangePicker = this.$createSegmentPicker({
        data: dateSegmentData,
        onSelect: (selectedDates, selectedVals, selectedTexts) => {
          this.$createDialog({
            type: 'warn',
            content: `Selected Items: <br/> - 开始时间: ${selectedTexts[0].join('')} <br/> - 结束时间: ${selectedTexts[1].join('')}`,
            icon: 'cubeic-alert'
          }).show()
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
    padding: 10px 0;
  }

  .input-text {
  }
}
</style>


