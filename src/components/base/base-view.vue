<template>
  <transition name="page-move">
    <router-view class="base-view"></router-view>
  </transition>
</template>

<script type="text/ecmascript-6">
export default {
  name: "base-view"
};
</script>

<style lang="stylus" rel="stylesheet/stylus">
.page-move-enter, .page-move-leave-active {
  transform: translate(100%, 0);
}

.page-move-enter-active, .page-move-leave-active {
  transition: transform 0.3s;
}
</style>
