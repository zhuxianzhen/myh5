<template>
    <section style="padding:12px 20px">
        <div class="style-item">
            <label>点击事件</label>
            <el-radio-group class="style-item" :value="data.type">
                <el-radio @change="updateItem({key: 'event', val: {type: 0 }})" :label="0">无</el-radio>
                <el-radio @change="updateItem({key: 'event', val: {type: 1 }})" :label="1">链接</el-radio>
                <el-radio @change="updateItem({key: 'event', val: {type: 2 }})" :label="2">电话</el-radio>
            </el-radio-group>
        </div>
        <div class="style-item" v-if="data.type == 1">
            <label>链接地址</label>
            <el-input :title="data.url" @input="updateItem({key: 'event', val: {url: $event }});" :value="data.url" placeholder="网址"></el-input>
        </div>
        <div class="style-item" v-else-if="data.type == 2">
            <label>手机/电话</label>
            <el-input @input="updateItem({key: 'event', val: {tel: $event }});" :value="data.tel" placeholder="010-88888888"></el-input>
        </div>
    </section>
</template>
<script>
import $ from "jquery";
import { mapActions, mapGetters } from "vuex";

export default {
    computed: {
        ...mapGetters(["curItem"]),
        data() {
            let event = this.curItem.event || {};
            if ($.isEmptyObject(event)) {
                event = {
                    type: 0,
                    url: "",
                    tel: ""
                };
            }
            return event;
        }
    },
    methods: {
        ...mapActions(["updateItem"])
    }
};
</script>

<style lang="scss" scoped>
.el-radio {
    line-height: 20px;
    font-size: 12px;
}
.style-item {
    padding: 8px 0;
    display: flex;
    align-items: center;
    justify-content: space-between;
}
.el-radio-group {
    flex-wrap: wrap;
}
</style>
