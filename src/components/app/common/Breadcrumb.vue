<template>
    <div class="clearfix">
        <el-breadcrumb separator-class="el-icon-arrow-right">
            <template v-for="item in levelList">
                <el-breadcrumb-item class="breadcrumb-item" v-if="item.path != '/app' && item.path != '/admin'" :key="item.path" :to="$route.path != item.path ? item.path : null" :class="$route.path == item.path ? 'current-path': ''">{{item.meta.title}}</el-breadcrumb-item>
            </template>
        </el-breadcrumb>
    </div>
</template>

<script>
export default {
    name: "app.common.breadcrumb",
    data() {
        return {
            levelList: []
        };
    },
    watch: {
        $route() {
            this.getBreadcrumb()
        }
    },
    created() {
        this.getBreadcrumb()
    },
    methods: {
        getBreadcrumb() {
            this.levelList = this.$route.matched
            // 导航到正确的地方
            this.levelList.forEach(route=>{
                if (route.meta.paramName){
                    route.path = route.path.replace(':'+route.meta.paramName, this.$route.params[route.meta.paramName])
                }
            });
        }
    }
};
</script>

<style lang="less" scoped>
.current-path > span{
    color: #909399 !important;
}
.breadcrumb-item{
    font-size: 20px;
    letter-spacing: 0.05em;
    user-select: none;
    -webkit-user-drag: none;
}
</style>
