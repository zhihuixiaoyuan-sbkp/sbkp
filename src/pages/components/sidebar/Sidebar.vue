<template>
    <div class="sider">
        <div class="sider-scroll">
            <!--default-active	当前激活菜单的 index-->
            <!--router	是否使用 vue-router 的模式，启用该模式会在激活导航时以 index 作为 path 进行路由跳转-->
            <el-menu :default-active="$route.path" router>
                <template v-for="issue in $router.options.routes">
                    <!-- 当该值与router的根路由的name相等时加载相应菜单组 -->
                    <template v-if="issue.name === $store.state.Sidebar">
                        <template v-for="item in issue.children">
                            <el-menu-item :index="item.path"
                                          :class="$route.path===item.path?'is-active':''" v-show="item.menuShow">
                                <span slot="title">{{item.name}}</span>
                            </el-menu-item>
                        </template>
                    </template>
                </template>
            </el-menu>
        </div>
    </div>
</template>

<script>
    export default {
        name: "Sidebar",
        data() {
            return {}
        },
        methods: {
            defaultLeftNavOpened() {
                let cur_path = this.$route.path; //获取当前路由
                let routers = this.$router.options.routes; // 获取路由对象
                for (let i = 0; i < routers.length; i++) {
                    let children = routers[i].children;
                    if (children) {
                        for (let j = 0; j < children.length; j++) {
                            if (children[j].path === cur_path) {
                                break;
                            }
                        }
                    }
                }
            },
        },
        mounted() {
            this.defaultLeftNavOpened();
        },
    }
</script>

<style scoped>
    .sider {
        position: absolute;
        top: 60px;
        bottom: 0;
        overflow: hidden;
        width: 180px;
        background: #303030;
    }

    .sider-scroll {
        overflow: hidden;
        width: 100%;
        height: 100%;
    }

    .el-menu {
        border: 0;
        background: #303030;
    }

    .el-menu-item, .el-submenu__title {
        height: 52px;
        color: #fff;
        line-height: 52px;
        border-left: 3px solid #303030;
    }

    .el-menu-item.is-active,
    .el-menu-item:hover,
    .el-submenu__title:hover,
    .el-menu-item:hover {
        /*background-color: rgba(43,56,128,0.4);*/
        /*border-left:3px solid #457aec;*/
        color: #fff;
        border-left: 3px solid #457aec;
        background-color: #1C1C1C;
    }
</style>