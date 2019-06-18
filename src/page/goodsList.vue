<template>
    <div class="page-product">
        <el-row class="m-crumbs">
            <crumbs />
        </el-row>
        <el-row>
            <el-col :span="19">
                <categroy />
                <el-row>
                    <list />
                </el-row>
            </el-col>
            <el-col :span="5">
                右边腾讯地图 + 猜你喜欢界面（省略）
            </el-col>            
        </el-row>
    </div>
</template>
<script>
import crumbs from '@/components/products/crumbs.vue'
import Categroy from '@/components/products/categroy.vue'
import List from '@/components/products/list.vue'
export default {
    components:{
        crumbs,
        Categroy,
        List
    }
}
</script>
<style lang="scss">
    @import "@/assets/css/products/index.scss"
</style>