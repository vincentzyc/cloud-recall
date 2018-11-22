<template>
    <div id="app">
        <div class="app-content">
            <RecallList />
            <footer class="footer flex relative">
                <div class="flex flex-auto flex-center border-r">
                    <span>我的回忆</span>
                </div>
                <div class="add-recall"></div>
                <div class="flex flex-auto flex-center">
                    <span>支出统计</span>
                </div>
            </footer>
        </div>
    </div>
</template>
<script>
// @ is an alias to /src
import RecallList from "@/components/RecallList.vue";
export default {
    name: "app",
    components: {
        RecallList
    }
    // mounted() {
    //     this.$nextTick(function() {
    //         window.addEventListener("load", () => {
    //             this.$refs.scroll.refresh();
    //         });
    //     });
    // }
};
</script>

<style>
#app,
body,
html {
    height: 100%;
}
.app-content {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    overflow: auto;
    -webkit-overflow-scrolling: touch;
}
.border-r{
    border-right: 1px solid #dedede
}
.footer {
    position: fixed;
    left: 0;
    bottom: 0;
    width: 100%;
    height: 50px;
    border-top: 1px solid #dedede;
    background: #fff;
}
.add-recall {
    position: absolute;
    top: -20px;
    left: 50%;
    margin-left: -25px;
    width: 52px;
    height: 52px;
    border: 1px solid #dedede;
    border-radius: 100%;
    background: #fff url("./assets//img/add.png") no-repeat center center/36px 36px;
    z-index: 999;
}
</style>
