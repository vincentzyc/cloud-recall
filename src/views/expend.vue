<template>
  <div slot="content">
    <ul class="mg10">
      <li class="flex pd10">
        <span>本周：</span>
        <span>{{weekStartDate}} 至 {{weekEndDate}}</span>
      </li>
      <li class="flex pd10">
        <span>本月：</span>
        <span>{{monthStartDate}} 至 {{monthEndDate}}</span>
      </li>
    </ul>
  </div>
</template>

<script type="text/ecmascript-6">
export default {
  data() {
    return {
      buttonStyle: ["inline", "outline", "primary"]
    };
  },
  computed: {
    weekStartDate() {
      return this.$util.getDate().getWeekStartDate();
    },
    weekEndDate() {
      return this.$util.getDate().getWeekEndDate();
    },
    monthStartDate() {
      return this.$util.getDate().getMonthStartDate();
    },
    monthEndDate() {
      return this.$util.getDate().getMonthEndDate();
    },
    inlineStyle() {
      return this.buttonStyle.indexOf("inline") >= 0;
    },
    outlineStyle() {
      return this.buttonStyle.indexOf("outline") >= 0;
    },
    primaryStyle() {
      return this.buttonStyle.indexOf("primary") >= 0;
    }
  }
};
</script>
