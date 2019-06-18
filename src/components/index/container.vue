<template>
    <div class="m-istyle">
        <dl @mouseover="over" :class="nav.class">
            <dt>{{nav.title}}</dt>
            <dd v-for="(item,index) in nav.list" :key="index" :class="{active:kind == item.tab}" 
                :data-type="item.type">{{item.text}}</dd>          
        </dl>
        <ul class="ibody">
            <li v-for="(item,index) in list" :key="index">
                <el-card :body-style="{ padding: '0px' }" shadow="never">
                    <img :src="item.image" class="image">
                    <div class="cbody">
                        <div class="title" :title="item.title">{{item.title}}</div>
                        <div class="sub-title" :title="item.sub_title">{{item.sub_title}}</div>
                        <div class="price-info" v-if="item.rentNum && item.price_info.current_price">
                            <span class="current-price-wrapper">
                                <span class="price-symbol numfont">¥</span>
                                <span class="current-price numfont">{{item.price_info.current_price}}</span>
                            </span>
                                <span class="old-price">门市价{{item.price_info.old_price}}</span>
                                <span class="sold bottom-right-info">{{item.address}}</span>
                        </div>
                        <div class="price-info" v-else-if="!item.rentNum">
                            <span class="current-price-wrapper">
                                <span class="price-symbol numfont">¥</span>
                                <span class="current-price numfont">抢光了</span>
                            </span>
                            <span class="sold bottom-right-info">{{item.address}}</span>
                        </div>
                        <div class="price-info" v-else>
                            <span class="current-price-wrapper">
                                <span class="price-symbol numfont">¥</span>
                                <span class="current-price numfont">{{item.price_info.avg_price}}</span>
                                <span class="units">/{{item.price_info.units}}</span>
                            </span>
                            <span class="sold bottom-right-info">{{item.address}}</span>
                        </div>
                    </div>
                </el-card>
            </li>
        </ul>
    </div>
</template>
<script>
import api from '@/api/index.js'
export default {
    data(){
        return {
            kind:"all",
            list:[{
                image:"//p0.meituan.net/bbia/d166c04ecdf18c055195bc87963254a3581920.png@368w_208h_1e_1c",
                title:"储缘蛋糕（留下镇店）",
                sub_title:"8英寸欧式水果生日蛋糕--领先推出蛋糕店送货上门贴心服务的理念",
                price_info:{
                    current_price:null,
                    old_price:null,
                    avg_price:100,
                    units:'人均'
                },
                rentNum:100,
                address:"留下"
            },{
                image:"//p1.meituan.net/msmerchant/8affb11c0530a8d1a2bb72b00ddb71ee32630.jpg@368w_208h_1e_1c",
                title:"浙江大酒店·中国蓝咖啡厅",
                sub_title:"一大一小自助晚餐",
                price_info:{
                    current_price:276,
                    old_price:402,
                    avg_price:null,
                    units:null
                },
                rentNum:100,
                address:"延安路沿线"
            },{
                image:"//p1.meituan.net/merchantpic/e592a58bf44d7192360d95e239fac823141726.jpg@240w_180h_1e_1c_1l|watermark=1&&r=2&p=9&x=2&y=2&relative=1&o=20|368w_208h_1e_1c",
                title:"别来无恙massage SPA",
                sub_title:"别来无恙massage SPA",
                price_info:{
                    current_price:null,
                    old_price:null,
                    avg_price:88,
                    units:'位'
                },
                rentNum:0,
                address:"西湖文化广场"
            },{
                image:"//p0.meituan.net/msmerchant/33ee2baaae1609942dd510f11193890843492.jpg@368w_208h_1e_1c",
                title:"新旺茶餐厅（嘉里中心店）",
                sub_title:"下午茶套餐，建议单人使用",
                price_info:{
                    current_price:30,
                    old_price:60,
                    avg_price:null,
                    units:null
                },
                rentNum:99,
                address:"嘉里中心"
            },{
                image:"//p0.meituan.net/msmerchant/df8ed3cc84b4de5321fff48c9c352b83789724.jpg@368w_208h_1e_1c",
                title:"必胜客（湖墅店）",
                sub_title:"【重磅拼盘饮料组合A012】1份人气重磅拼盘+2份葡萄柚韵香气泡乌龙茶（冰/温）1份",
                price_info:{
                    current_price:88,
                    old_price:113,
                    avg_price:null,
                    units:null
                },
                rentNum:199,
                address:"湖墅南路"
            },{
                image:"//p0.meituan.net/bbia/5d1920d0a21a75b47beaec65d09ddc3c1938758.jpg@368w_208h_1e_1c",
                title:"非凡酒廊大堂吧（城中香格里拉大酒店）",
                sub_title:"煦日花开下午茶",
                price_info:{
                    current_price:268,
                    old_price:300,
                    avg_price:null,
                    units:null
                },
                rentNum:199,
                address:"嘉里中心"
            }]
        }
    },
    props:[
        'nav'
    ],
    created(){
        api.getResultProducts().then(res => {
            console.log(res);
        })
    },
    methods:{
        over(e){
            let dom = e.target;
            let tagName = dom.tagName.toLowerCase();
            if(tagName != 'dd'){
                return false;
            }
            this.kind = dom.getAttribute('data-type');
            //动态获取数据 ajax请求
        }
    }
}
</script>
<style lang="scss">
    @import "@/assets/css/index/artistic.scss";
</style>
