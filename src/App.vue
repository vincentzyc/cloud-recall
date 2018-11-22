<template>
    <div id="app">
        <div class="app-content">
            <RecallList />
            <footer class="footer">
                <cube-tab-bar v-model="selectedLabelDefault" :data="tabs" @click="clickHandler"></cube-tab-bar>
                <div class="add-recall"></div>
            </footer>
        </div>
    </div>
</template>
<script>
// @ is an alias to /src
import RecallList from "@/components/RecallList.vue";
export default {
    name: "app",
    data() {
        return {
            tab_active: "recall",
            selectedLabelDefault: "我的回忆",
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
    components: {
        RecallList
    },
    methods: {
        clickHandler(label) {
            // if you clicked home tab, then print 'Home'
            console.log(label);
        }
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
    z-index: 0;
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
.border-r {
    border-right: 1px solid #dedede;
}
.active {
    background: #666;
    color: #fff;
}
.footer {
    position: relative;
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
    margin-left: -25px;
    width: 52px;
    height: 52px;
    border: 1px solid #dedede;
    border-radius: 100%;
    background: #fff url("./assets//img/add.png") no-repeat center center/36px 36px;
}
</style>
