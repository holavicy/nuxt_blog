
<template>
    <div class="page-activity">
        <div v-show="tabNavFixed" class="tab-list fixed">
            <div class="item" v-for="tab in tabList" :key="tab.id" :class="{active: currentTab === tab.id}"  @click="scrollToTab(tab.id)">{{tab.name}}</div>
        </div>
        <div ref="scrollContainer">
            <div class="container">
                <div class="activity-banner">
                    <img ref="banner" src="https://image3.vipmro.net/mpImg/smb/activity_banner.png">
                </div>

                <div ref="tabNav" class="tab-nav">
                    <div class="tab-list">
                        <div class="item" v-for="tab in tabList" :key="tab.id" :class="{active: currentTab === tab.id}"  @click="scrollToTab(tab.id)">{{tab.name}}</div>
                    </div>
                </div>

                <template v-if="tabList.length && !loading">
                    <div class="tab-items">
                        <div v-for="tab in tabList" :key="tab.id" :id="'tab_' + tab.id" :data-id="tab.id" class="tab-container">
                            <div class="tab-title">
                                <label class="title">{{tab.name}}</label>
                            </div>
                            <div class="tab-content">
                                <a
                                    v-for="(goods, index) in tab.goodsList"
                                    :key="index"
                                    :href="env === 'web' ? 'javascript: void 0;' : `vipmromall://Mall_goods_detail?sellerGoodsId=${goods.sellerGoodsId}`"
                                    class="m-goods-item"
                                    @click="toGoodsPage(goods.sellerGoodsId)"
                                >
                                    <div class="goods-thumb">
                                        <div v-if="goods.isSaleLimit === 1" class="tag-presell">预售</div>
                                        <img class="thumb" :src="goods.image ">
                                    </div>
                                    <div class="goods-info">
                                        <div class="title">{{goods.goodsName}}</div>
                                        <div class="infos">
                                            <div class="item">型号：{{goods.model}}</div>
                                            <div class="item">订货号：{{goods.buyNo}}</div>
                                        </div>
                                        <div class="price">￥ {{goods.price}}</div>
                                        <div class="buy-btn">
                                            <i class="icon"></i> 立即购买
                                        </div>
                                    </div>
                                </a>
                            </div>
                        </div>
                    </div>
                    <div class="page-bottom">—— 到底啦 ——</div>
                </template>
                <!-- <base-empty v-else-if="!loading" :icon="2" tip="暂无相关商品"></base-empty> -->
            </div>
        </div>
        <div v-if="env !== 'web'" class="page-share-btn" @click="sharePage">
            <!-- <img class="icon" src="./images/share@2x.png"> -->
            <label class="title">去分享</label>
        </div>
        <a v-if="scrollTopShow" href="javascript: void 0;" class="page-totop" @click="scrollToTop"></a>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                // ios微信webview环境包含window.webkit，故无法通过window.webkit判断当前环境为ios
                env: window.webkit && this.$route.query.iosVersion ? 'ios' : window.jsCallAndroid ?  'android' : 'web',
                loading: false,
                tabList: [],
                currentTab: '',
                tabNavFixed: false,
                scrollTopShow: false,
                tabPositions: [],
                tabNavTop: 0,
                tabNavHeight: 0
            }
        },
        mounted() {
            this.loadData();
            let banner = this.$refs.banner;
            banner.onload = () => {
                this.$refs.scrollContainer.refresh();
                this.$nextTick().then(() => {
                    this.adjustDomPositionData();
                })
            }
        },
        methods: {
            loadData() {
       let res = {
        code:0,
        msg:'',
        data:{
          name:'b2r专题',
          style: {
                  "bgColor": "#FF00FF",
                  "topImg": "http://image3.vipmro.net/mpImg/yqzt_bg.png",

                  "tabChooseColor": "#00ff42",
                  "tabChooseFontColor": "#2335eb",
                  "tabChooseAlpha":'20',
                  "tabChooseBgImg": "https://image3.vipmro.net/mallAdver/4e94d531-4998-4ecd-a46f-3e44b1ed4a6d.png",

                  "titleFontColor":"#e5e5e5",
                  "titleBgColor": "#FF00BC",
                  "titleAlpha": "10",
                  "titleBgImg": "https://image3.vipmro.net/mallAdver/25f2f379-67c4-4357-acbf-79656a6aef6f.png",

                  "titleRightImg": "https://image3.vipmro.net/mallAdver/4e94d531-4998-4ecd-a46f-3e44b1ed4a6d.png",
                  "titleLeftImg": "https://image3.vipmro.net/mallAdver/4e94d531-4998-4ecd-a46f-3e44b1ed4a6d.png",

                  "buyBgColor": "#0016ff",
              },

              list:[
                {
                    "name": "洁净除菌洁净 ",
                    "goodsList": [{
                        "image": "https://image.vipmro.net/goodsImg//999999/701411/01818/202003061550/001a01.jpg",
                        "salePrice": null,
                        "cateId": 701411,
                        "goodsId": 1228607182971469825,
                        "brandId": 6915,
                        "model": "免洗手抗菌凝胶120ml",
                        "sellerGoodsId": 79405404,
                        "buyNo": "SD200215120",
                        "goodsName": "三盾 免洗手抗菌凝胶120ml",
                        "isSaleLimit": 0
                    }, {
                        "image": "https://image.vipmro.net/goodsImg//group1/M00/57/13/wKigOF42jCSAQ9x4AAGAMBY09dU710.jpg",
                        "salePrice": null,
                        "cateId": 60154008,
                        "goodsId": 1223889705213493250,
                        "brandId": 6886,
                        "model": "SYI0001",
                        "sellerGoodsId": 79403872,
                        "buyNo": "SYI0001",
                        "goodsName": "苏阿姨 84消毒液600ml,有效氯含量：2.5-5%。；SYI0001",
                        "isSaleLimit": 0
                    }, {
                        "image": "https://image.vipmro.net/goodsImg/999999/701519/01818/202003061550/002a01.jpg",
                        "salePrice": null,
                        "cateId": 60154008,
                        "goodsId": 1225699512652267521,
                        "brandId": 6907,
                        "model": "LEEDUN-50ml-免洗",
                        "sellerGoodsId": 79404705,
                        "buyNo": "LEEDUN-50ml",
                        "goodsName": "LEEDUN莱盾 50ml免洗抑菌洗手液,泡沫型(0.1%苯扎氯铵),48瓶/箱；LEEDUN-50ml-免洗",
                        "isSaleLimit": 0
                    }, {
                        "image": "https://image.vipmro.net/goodsImg/999999/701519/01818/202003061550/001a01.jpg",
                        "salePrice": null,
                        "cateId": 60154008,
                        "goodsId": 1227521651604848642,
                        "brandId": 6910,
                        "model": "DGMXNJ0050",
                        "sellerGoodsId": 79404037,
                        "buyNo": "DGMXNJ0050",
                        "goodsName": "涤高 免洗手酒精消毒凝胶(便携,凝胶型)50g/瓶,25瓶/盒；DGMXNJ0050",
                        "isSaleLimit": 0
                    }, {
                        "image": "https://image.vipmro.net/goodsImg/999999/102911/00025/202002181523/001a01.jpg",
                        "salePrice": null,
                        "cateId": 701411,
                        "goodsId": 1229593486421000193,
                        "brandId": 6923,
                        "model": "DAA048",
                        "sellerGoodsId": 79404201,
                        "buyNo": "DAA048",
                        "goodsName": "爱生活 抑菌免洗净手凝露 75ml；DAA048",
                        "isSaleLimit": 0
                    }, {
                        "image": "https://image.vipmro.net/goodsImg/999999/102911/00025/20200216161/001a01.jpg",
                        "salePrice": null,
                        "cateId": 60154008,
                        "goodsId": 1227828986466402305,
                        "brandId": 6923,
                        "model": "ASH0001",
                        "sellerGoodsId": 79404069,
                        "buyNo": "ASH0001",
                        "goodsName": "爱生活 84消毒液1kg,有效氯含量：6.45%；ASH0001",
                        "isSaleLimit": 0
                    }, {
                        "image": "https://image.vipmro.net/goodsImg/999999/701510/01818/202003061550/001a01.jpg",
                        "salePrice": null,
                        "cateId": 701510,
                        "goodsId": 1227459829237415938,
                        "brandId": 6904,
                        "model": "SA-628",
                        "sellerGoodsId": 79404024,
                        "buyNo": "SA-628",
                        "goodsName": "斯瑞 一次性医用酒精消毒棉片65x56mm,100片/盒,100盒/箱；SA-628",
                        "isSaleLimit": 0
                    }, {
                        "image": "https://image.vipmro.net/goodsImg//group1/M00/57/90/wKigOV4-dxuAAz8UAAMGJtoE2n4196.jpg",
                        "salePrice": null,
                        "cateId": 60154008,
                        "goodsId": 1224244461794623490,
                        "brandId": 6888,
                        "model": "QBXDY",
                        "sellerGoodsId": 79403895,
                        "buyNo": "QBXDY",
                        "goodsName": "乾宝 次氯酸钠消毒液,20L桶装,PH呈中性,可10倍稀释,有效氯含量：50-150mg/L；QBXDY",
                        "isSaleLimit": 0
                    }, {
                        "image": "https://image.vipmro.net/goodsImg/999999/10291/00025/202002121729/003a01.jpg",
                        "salePrice": null,
                        "cateId": 60154008,
                        "goodsId": 1227170815167037442,
                        "brandId": 6915,
                        "model": "免洗180ml",
                        "sellerGoodsId": 79404019,
                        "buyNo": "SD200210001",
                        "goodsName": "三盾 医用级杀菌免洗手消毒液180ml,(0.1%苯扎氯铵)；免洗180ml",
                        "isSaleLimit": 0
                    }, {
                        "image": "https://image.vipmro.net/goodsImg//999999/10291/00025/202002121729/001a01.jpg",
                        "salePrice": null,
                        "cateId": 60154008,
                        "goodsId": 1227144599596826626,
                        "brandId": 6914,
                        "model": "SYT0001",
                        "sellerGoodsId": 79404010,
                        "buyNo": "SYT0001",
                        "goodsName": "苏韵堂 免洗手消毒液,医护级,杀菌率99.999% 75ml+15ml；SYT0001",
                        "isSaleLimit": 0
                    }, {
                        "image": "https://image.vipmro.net/goodsImg/999999/102911/00025/202002131000/005a01.jpg",
                        "salePrice": null,
                        "cateId": 701717,
                        "goodsId": 1227567067067187201,
                        "brandId": 2,
                        "model": "FSMH1300FX",
                        "sellerGoodsId": 79404041,
                        "buyNo": "FSMH1300FX-A9",
                        "goodsName": "史丹利 百得高温杀菌蒸汽拖把,清洁机；FSMH1300FX-A9",
                        "isSaleLimit": 0
                    }, {
                        "image": "https://image.vipmro.net/goodsImg/999999/701512/00025/202002190936/001a01.jpg",
                        "salePrice": null,
                        "cateId": 60154008,
                        "goodsId": 1156735780031430677,
                        "brandId": 1859,
                        "model": "80600620208",
                        "sellerGoodsId": 79343227,
                        "buyNo": "80600620208",
                        "goodsName": "立白 威王84消毒液清洁大礼包，有效氯含量：1-1.35%；80600620208",
                        "isSaleLimit": 0
                    }, {
                        "image": "https://image.vipmro.net/goodsImg//group1/M00/57/18/wKigOF43hhKANKd1AAFS_j1kyps737.jpg",
                        "salePrice": null,
                        "cateId": 701411,
                        "goodsId": 1223525394876071938,
                        "brandId": 3702,
                        "model": "hbeb128d",
                        "sellerGoodsId": 79403934,
                        "buyNo": "hbeb128d",
                        "goodsName": "隆力奇 洋甘菊泡沫洗手液5KG；hbeb128d",
                        "isSaleLimit": 0
                    }, {
                        "image": "https://image.vipmro.net/goodsImg//group1/M00/58/53/wKigOF5HZHSAGXRyAAJznvDl-P0198.jpg",
                        "salePrice": null,
                        "cateId": 701510,
                        "goodsId": 1224901690378027010,
                        "brandId": 6898,
                        "model": "SJwssj",
                        "sellerGoodsId": 79403922,
                        "buyNo": "SJwssj",
                        "goodsName": "舒捷 医用级别卫生湿巾(杀菌率99.9%)80片/包",
                        "isSaleLimit": 0
                    }, {
                        "image": "https://image.vipmro.net/goodsImg//group1/M00/57/59/wKigOF48JnqARlTCAAHOL3n3ZeE975.jpg",
                        "salePrice": null,
                        "cateId": 701617,
                        "goodsId": 1225347160996970498,
                        "brandId": 6902,
                        "model": "MH-2.0",
                        "sellerGoodsId": 79403941,
                        "buyNo": "MH-2.0",
                        "goodsName": "美化 手动喷雾器 2L；MH-2.0",
                        "isSaleLimit": 0
                    }, {
                        "image": "https://image.vipmro.net/goodsImg//group1/M00/57/F4/wKigOF5CmO2AJ43VAAGOQTducWc750.jpg",
                        "salePrice": null,
                        "cateId": 60154008,
                        "goodsId": 1224228194660515843,
                        "brandId": 6887,
                        "model": "6956907411231",
                        "sellerGoodsId": 79403893,
                        "buyNo": "6956907411231",
                        "goodsName": "优护优家 抗菌免洗手凝露50ml",
                        "isSaleLimit": 0
                    }, {
                        "image": "https://image.vipmro.net/goodsImg//group1/M00/57/2E/wKigOF45JLCAS78oAAFKnzqHdEk234.jpg",
                        "salePrice": null,
                        "cateId": 60154008,
                        "goodsId": 1232957134287798274,
                        "brandId": 6887,
                        "model": "6956907410364",
                        "sellerGoodsId": 79405652,
                        "buyNo": "6956907410364",
                        "goodsName": "优护优家 空气物表消毒液460ml,喷雾型(0.11-0.13%复合季铵盐)；6956907410364",
                        "isSaleLimit": 0
                    }],
                    "id": 4
                },
                {
                    "name": "cxzcxzcxz ",
                    "goodsList": [{
                        "image": "https://image.vipmro.net/goodsImg//999999/701411/01818/202003061550/001a01.jpg",
                        "salePrice": null,
                        "cateId": 701411,
                        "goodsId": 1228607182971469825,
                        "brandId": 6915,
                        "model": "免洗手抗菌凝胶120ml",
                        "sellerGoodsId": 79405404,
                        "buyNo": "SD200215120",
                        "goodsName": "三盾 免洗手抗菌凝胶120ml",
                        "isSaleLimit": 0
                    }],
                    "id": 16
                },
                {
                    "name": "大萨达撒多撒大所多撒多撒多撒 ",
                    "goodsList": [{
                        "image": "https://image.vipmro.net/goodsImg//999999/701411/01818/202003061550/001a01.jpg",
                        "salePrice": null,
                        "cateId": 701411,
                        "goodsId": 1228607182971469825,
                        "brandId": 6915,
                        "model": "免洗手抗菌凝胶120ml",
                        "sellerGoodsId": 79405404,
                        "buyNo": "SD200215120",
                        "goodsName": "三盾 免洗手抗菌凝胶120ml",
                        "isSaleLimit": 0
                    }, {
                        "image": "https://image.vipmro.net/goodsImg//group1/M00/57/13/wKigOF42jCSAQ9x4AAGAMBY09dU710.jpg",
                        "salePrice": null,
                        "cateId": 60154008,
                        "goodsId": 1223889705213493250,
                        "brandId": 6886,
                        "model": "SYI0001",
                        "sellerGoodsId": 79403872,
                        "buyNo": "SYI0001",
                        "goodsName": "苏阿姨 84消毒液600ml,有效氯含量：2.5-5%。；SYI0001",
                        "isSaleLimit": 0
                    }, {
                        "image": "https://image.vipmro.net/goodsImg/999999/701519/01818/202003061550/002a01.jpg",
                        "salePrice": null,
                        "cateId": 60154008,
                        "goodsId": 1225699512652267521,
                        "brandId": 6907,
                        "model": "LEEDUN-50ml-免洗",
                        "sellerGoodsId": 79404705,
                        "buyNo": "LEEDUN-50ml",
                        "goodsName": "LEEDUN莱盾 50ml免洗抑菌洗手液,泡沫型(0.1%苯扎氯铵),48瓶/箱；LEEDUN-50ml-免洗",
                        "isSaleLimit": 0
                    }, {
                        "image": "https://image.vipmro.net/goodsImg/999999/701519/01818/202003061550/001a01.jpg",
                        "salePrice": null,
                        "cateId": 60154008,
                        "goodsId": 1227521651604848642,
                        "brandId": 6910,
                        "model": "DGMXNJ0050",
                        "sellerGoodsId": 79404037,
                        "buyNo": "DGMXNJ0050",
                        "goodsName": "涤高 免洗手酒精消毒凝胶(便携,凝胶型)50g/瓶,25瓶/盒；DGMXNJ0050",
                        "isSaleLimit": 0
                    }, {
                        "image": "https://image.vipmro.net/goodsImg/999999/102911/00025/202002181523/001a01.jpg",
                        "salePrice": null,
                        "cateId": 701411,
                        "goodsId": 1229593486421000193,
                        "brandId": 6923,
                        "model": "DAA048",
                        "sellerGoodsId": 79404201,
                        "buyNo": "DAA048",
                        "goodsName": "爱生活 抑菌免洗净手凝露 75ml；DAA048",
                        "isSaleLimit": 0
                    }, {
                        "image": "https://image.vipmro.net/goodsImg/999999/102911/00025/20200216161/001a01.jpg",
                        "salePrice": null,
                        "cateId": 60154008,
                        "goodsId": 1227828986466402305,
                        "brandId": 6923,
                        "model": "ASH0001",
                        "sellerGoodsId": 79404069,
                        "buyNo": "ASH0001",
                        "goodsName": "爱生活 84消毒液1kg,有效氯含量：6.45%；ASH0001",
                        "isSaleLimit": 0
                    }, {
                        "image": "https://image.vipmro.net/goodsImg/999999/701510/01818/202003061550/001a01.jpg",
                        "salePrice": null,
                        "cateId": 701510,
                        "goodsId": 1227459829237415938,
                        "brandId": 6904,
                        "model": "SA-628",
                        "sellerGoodsId": 79404024,
                        "buyNo": "SA-628",
                        "goodsName": "斯瑞 一次性医用酒精消毒棉片65x56mm,100片/盒,100盒/箱；SA-628",
                        "isSaleLimit": 0
                    }],
                    "id": 15
                },
                {
                    "name": "大萨达撒大所 ",
                    "goodsList": [{
                        "image": "https://image.vipmro.net/goodsImg//999999/701411/01818/202003061550/001a01.jpg",
                        "salePrice": null,
                        "cateId": 701411,
                        "goodsId": 1228607182971469825,
                        "brandId": 6915,
                        "model": "免洗手抗菌凝胶120ml",
                        "sellerGoodsId": 79405404,
                        "buyNo": "SD200215120",
                        "goodsName": "三盾 免洗手抗菌凝胶120ml",
                        "isSaleLimit": 0
                    }],
                    "id": 14
                },
                {
                    "name": "大萨达撒多撒 ",
                    "goodsList": [{
                        "image": "https://image.vipmro.net/goodsImg//999999/701411/01818/202003061550/001a01.jpg",
                        "salePrice": null,
                        "cateId": 701411,
                        "goodsId": 1228607182971469825,
                        "brandId": 6915,
                        "model": "免洗手抗菌凝胶120ml",
                        "sellerGoodsId": 79405404,
                        "buyNo": "SD200215120",
                        "goodsName": "三盾 免洗手抗菌凝胶120ml",
                        "isSaleLimit": 0
                    }, {
                        "image": "https://image.vipmro.net/goodsImg//group1/M00/57/13/wKigOF42jCSAQ9x4AAGAMBY09dU710.jpg",
                        "salePrice": null,
                        "cateId": 60154008,
                        "goodsId": 1223889705213493250,
                        "brandId": 6886,
                        "model": "SYI0001",
                        "sellerGoodsId": 79403872,
                        "buyNo": "SYI0001",
                        "goodsName": "苏阿姨 84消毒液600ml,有效氯含量：2.5-5%。；SYI0001",
                        "isSaleLimit": 0
                    }, {
                        "image": "https://image.vipmro.net/goodsImg/999999/701519/01818/202003061550/002a01.jpg",
                        "salePrice": null,
                        "cateId": 60154008,
                        "goodsId": 1225699512652267521,
                        "brandId": 6907,
                        "model": "LEEDUN-50ml-免洗",
                        "sellerGoodsId": 79404705,
                        "buyNo": "LEEDUN-50ml",
                        "goodsName": "LEEDUN莱盾 50ml免洗抑菌洗手液,泡沫型(0.1%苯扎氯铵),48瓶/箱；LEEDUN-50ml-免洗",
                        "isSaleLimit": 0
                    }, {
                        "image": "https://image.vipmro.net/goodsImg/999999/701519/01818/202003061550/001a01.jpg",
                        "salePrice": null,
                        "cateId": 60154008,
                        "goodsId": 1227521651604848642,
                        "brandId": 6910,
                        "model": "DGMXNJ0050",
                        "sellerGoodsId": 79404037,
                        "buyNo": "DGMXNJ0050",
                        "goodsName": "涤高 免洗手酒精消毒凝胶(便携,凝胶型)50g/瓶,25瓶/盒；DGMXNJ0050",
                        "isSaleLimit": 0
                    }],
                    "id": 13
                },
                {
                    "name": "测测测测测测 ",
                    "goodsList": [{
                        "image": "https://image.vipmro.net/goodsImg//999999/701411/01818/202003061550/001a01.jpg",
                        "salePrice": null,
                        "cateId": 701411,
                        "goodsId": 1228607182971469825,
                        "brandId": 6915,
                        "model": "免洗手抗菌凝胶120ml",
                        "sellerGoodsId": 79405404,
                        "buyNo": "SD200215120",
                        "goodsName": "三盾 免洗手抗菌凝胶120ml",
                        "isSaleLimit": 0
                    }, {
                        "image": "https://image.vipmro.net/goodsImg//group1/M00/57/13/wKigOF42jCSAQ9x4AAGAMBY09dU710.jpg",
                        "salePrice": null,
                        "cateId": 60154008,
                        "goodsId": 1223889705213493250,
                        "brandId": 6886,
                        "model": "SYI0001",
                        "sellerGoodsId": 79403872,
                        "buyNo": "SYI0001",
                        "goodsName": "苏阿姨 84消毒液600ml,有效氯含量：2.5-5%。；SYI0001",
                        "isSaleLimit": 0
                    }, {
                        "image": "https://image.vipmro.net/goodsImg/999999/701519/01818/202003061550/002a01.jpg",
                        "salePrice": null,
                        "cateId": 60154008,
                        "goodsId": 1225699512652267521,
                        "brandId": 6907,
                        "model": "LEEDUN-50ml-免洗",
                        "sellerGoodsId": 79404705,
                        "buyNo": "LEEDUN-50ml",
                        "goodsName": "LEEDUN莱盾 50ml免洗抑菌洗手液,泡沫型(0.1%苯扎氯铵),48瓶/箱；LEEDUN-50ml-免洗",
                        "isSaleLimit": 0
                    }, {
                        "image": "https://image.vipmro.net/goodsImg/999999/701519/01818/202003061550/001a01.jpg",
                        "salePrice": null,
                        "cateId": 60154008,
                        "goodsId": 1227521651604848642,
                        "brandId": 6910,
                        "model": "DGMXNJ0050",
                        "sellerGoodsId": 79404037,
                        "buyNo": "DGMXNJ0050",
                        "goodsName": "涤高 免洗手酒精消毒凝胶(便携,凝胶型)50g/瓶,25瓶/盒；DGMXNJ0050",
                        "isSaleLimit": 0
                    }, {
                        "image": "https://image.vipmro.net/goodsImg/999999/102911/00025/202002181523/001a01.jpg",
                        "salePrice": null,
                        "cateId": 701411,
                        "goodsId": 1229593486421000193,
                        "brandId": 6923,
                        "model": "DAA048",
                        "sellerGoodsId": 79404201,
                        "buyNo": "DAA048",
                        "goodsName": "爱生活 抑菌免洗净手凝露 75ml；DAA048",
                        "isSaleLimit": 0
                    }, {
                        "image": "https://image.vipmro.net/goodsImg/999999/102911/00025/20200216161/001a01.jpg",
                        "salePrice": null,
                        "cateId": 60154008,
                        "goodsId": 1227828986466402305,
                        "brandId": 6923,
                        "model": "ASH0001",
                        "sellerGoodsId": 79404069,
                        "buyNo": "ASH0001",
                        "goodsName": "爱生活 84消毒液1kg,有效氯含量：6.45%；ASH0001",
                        "isSaleLimit": 0
                    }, {
                        "image": "https://image.vipmro.net/goodsImg/999999/701510/01818/202003061550/001a01.jpg",
                        "salePrice": null,
                        "cateId": 701510,
                        "goodsId": 1227459829237415938,
                        "brandId": 6904,
                        "model": "SA-628",
                        "sellerGoodsId": 79404024,
                        "buyNo": "SA-628",
                        "goodsName": "斯瑞 一次性医用酒精消毒棉片65x56mm,100片/盒,100盒/箱；SA-628",
                        "isSaleLimit": 0
                    }],
                    "id": 12
                },
                {
                    "name": "身体防护 ",
                    "goodsList": [{
                        "image": "https://image.vipmro.net/goodsImg//999999/701411/01818/202003061550/001a01.jpg",
                        "salePrice": null,
                        "cateId": 701411,
                        "goodsId": 1228607182971469825,
                        "brandId": 6915,
                        "model": "免洗手抗菌凝胶120ml",
                        "sellerGoodsId": 79405404,
                        "buyNo": "SD200215120",
                        "goodsName": "三盾 免洗手抗菌凝胶120ml",
                        "isSaleLimit": 0
                    }, {
                        "image": "https://image.vipmro.net/goodsImg//group1/M00/57/13/wKigOF42jCSAQ9x4AAGAMBY09dU710.jpg",
                        "salePrice": null,
                        "cateId": 60154008,
                        "goodsId": 1223889705213493250,
                        "brandId": 6886,
                        "model": "SYI0001",
                        "sellerGoodsId": 79403872,
                        "buyNo": "SYI0001",
                        "goodsName": "苏阿姨 84消毒液600ml,有效氯含量：2.5-5%。；SYI0001",
                        "isSaleLimit": 0
                    }, {
                        "image": "https://image.vipmro.net/goodsImg/999999/701519/01818/202003061550/002a01.jpg",
                        "salePrice": null,
                        "cateId": 60154008,
                        "goodsId": 1225699512652267521,
                        "brandId": 6907,
                        "model": "LEEDUN-50ml-免洗",
                        "sellerGoodsId": 79404705,
                        "buyNo": "LEEDUN-50ml",
                        "goodsName": "LEEDUN莱盾 50ml免洗抑菌洗手液,泡沫型(0.1%苯扎氯铵),48瓶/箱；LEEDUN-50ml-免洗",
                        "isSaleLimit": 0
                    }],
                    "id": 11
                },
                {
                    "name": "更多防护 ",
                    "goodsList": [{
                        "image": "https://image.vipmro.net/goodsImg//999999/701411/01818/202003061550/001a01.jpg",
                        "salePrice": null,
                        "cateId": 701411,
                        "goodsId": 1228607182971469825,
                        "brandId": 6915,
                        "model": "免洗手抗菌凝胶120ml",
                        "sellerGoodsId": 79405404,
                        "buyNo": "SD200215120",
                        "goodsName": "三盾 免洗手抗菌凝胶120ml",
                        "isSaleLimit": 0
                    }, {
                        "image": "https://image.vipmro.net/goodsImg//group1/M00/57/13/wKigOF42jCSAQ9x4AAGAMBY09dU710.jpg",
                        "salePrice": null,
                        "cateId": 60154008,
                        "goodsId": 1223889705213493250,
                        "brandId": 6886,
                        "model": "SYI0001",
                        "sellerGoodsId": 79403872,
                        "buyNo": "SYI0001",
                        "goodsName": "苏阿姨 84消毒液600ml,有效氯含量：2.5-5%。；SYI0001",
                        "isSaleLimit": 0
                    }],
                    "id": 10
                }
              ]
        }
      };

                    let tabList = this.tabList = (res.data.list || []).map(item => {
                        item.id = String(item.id);
                        return item
                    });
                    this.currentTab = tabList[0] && tabList[0].id || '';
                    this.$nextTick().then(() => {
                        this.tabElements = tabList.map(tab => document.getElementById('tab_'+tab.id)).filter(Boolean);
                        this.adjustDomPositionData();
                    })




                // this.loading = true;
                // this.$api('/activity/getThematicActivityData', {
                //     data: {
                //         mark: '2020fyzt'
                //     },
                //     loading: true
                // }).then(res => {
                //     this.loading= false;
                //     let tabList = this.tabList = (res.data || []).map(item => {
                //         item.id = String(item.id);
                //         return item
                //     });
                //     this.currentTab = tabList[0] && tabList[0].id || '';
                //     this.$nextTick().then(() => {
                //         this.tabElements = tabList.map(tab => document.getElementById('tab_'+tab.id)).filter(Boolean);
                //         this.adjustDomPositionData();
                //     })
                // }).catch(e => {
                //     this.loading = false;
                // })
            },
            toGoodsPage(id) {
                if(this.env === 'web') {
                    this.$router.push({name: 'Product', query: {productId: id}})
                }
            },
            scrollToTop() {
                this.$refs.scrollContainer.scrollYTo(0, 200);
            },
            scrollToTab(id) {
                let {clientHeight: tabNavHeight} = this.$refs.tabNav;
                let tab = document.getElementById('tab_'+id);
                if(tab) {
                    this.$refs.scrollContainer.scrollYTo(tab.offsetTop - tabNavHeight + 10, 200);
                    this.currentTab = id;
                }
            },
            adjustDomPositionData() {
                let {offsetTop, clientHeight} = this.$refs.tabNav;
                this.tabNavTop = offsetTop;
                this.tabNavHeight = clientHeight;
                this.tabPositions = this.tabElements.map(ele => {
                    return {
                        id: ele.dataset.id,
                        top: ele.offsetTop,
                        bottom: ele.offsetTop + ele.clientHeight
                    }
                });
            },
            wrapperScroll({y: scrollTop, dirY}) {
                // let {offsetTop: tabNavTop, clientHeight: tabNavHeight} = this.$refs.tabNav;

                this.scrollTopShow = this.tabNavFixed = scrollTop > this.tabNavTop;

                let tabs = this.tabPositions;
                let currentTab = tabs[0] && tabs[0].id || '';
                for(let i=0, len=tabs.length; i < len; i++) {
                    let current = tabs[i];
                    let next = tabs[i+1];
                    if (current.top - this.tabNavHeight < scrollTop) {
                        if(!next || (next && scrollTop < next.top - this.tabNavHeight)) {
                            currentTab = current.id;
                            break;
                        }
                    }
                }

                // let tabs = this.tabElements;
                // let currentTab = tabs[0] && tabs[0].dataset.id || '';
                // for(let i=0, len=tabs.length; i < len; i++) {
                //     let current = tabs[i];
                //     let next = tabs[i+1];
                //     if (current.offsetTop - this.tabNavHeight < scrollTop) {
                //         if(!next || (next && scrollTop < next.offsetTop - this.tabNavHeight)) {
                //             currentTab = current.dataset.id;
                //             break;
                //         }
                //     }
                // }
                this.currentTab = currentTab;
            },
            sharePage() {
                this.$util.appSharePage({
                    url: window.location.href.replace(/\??iosVersion=[^&]*&?/, ''),
                    title: '装备齐全，复工不难',
                    description: '【工品汇】助您做好疫情防护，从容应对复工',
                    thumbnailImage: 'https://image3.vipmro.net/mpImg/smb/activity_banner.png'
                });
            }
        }
    };
</script>


<style lang="less" scoped>

.page-activity {
    background: #f4f4f4;
}

.activity-banner img{
  width: 100%;
  vertical-align: top;
}

.tab-nav {
    height: 2.6667rem;
}

.tab-list {
    display: flex;
    flex-wrap: nowrap;
    overflow-x: auto;
    background: #fff;
    &::-webkit-scrollbar {
        display: none;
    }
    &.fixed {
        position: absolute;
        top: 0;
        left: 0;
        right: 0;
        z-index: 99;
    }
    .item {
        flex: 1 1 auto;
        height: 2.6667rem;
        padding: 0 1rem;
        line-height: 2.6667rem;
        white-space: nowrap;
        text-align: center;
        font-size: 0.9333rem;
        color: #222;
        transition: 0.2s;
        &.active {
            background: #D0021B;
            color: #fff;
        }
    }
}

.tab-title {
    padding: 1.3333rem 0;
    text-align: center;
    .title {
        position: relative;
        display: inline-block;
        height: 2rem;
        line-height: 2rem;
        padding: 0 1.3333rem;
        border-radius: 1rem;
        vertical-align: middle;
        background-color: #D0021B;
        font-size: 0.9333rem;
        color: #fff;
        &::before {
            content: '';
            position: absolute;
            left: -4.1667rem;
            top: 50%;
            transform: translateY(-50%);
            height: 1.0667rem;
            width: 3.5rem;
            // background: url(./images/line_left.png) no-repeat center center;
            background-size: contain;
        }
        &::after {
            content: '';
            position: absolute;
            right: -4.1667rem;
            top: 50%;
            transform: translateY(-50%);
            height: 1.0667rem;
            width: 3.5rem;
            // background: url(./images/line_right.png) no-repeat center center;
            background-size: contain;
        }
    }
}

.tab-content {
    padding: 0 0.6667rem;
}
.m-goods-item {
    display: flex;
    flex-wrap: nowrap;
    margin-top: 0.6667rem;
    padding: 0.6667rem;
    background: #fff;
    border-radius: 0.6667rem;
    &:first-child {
        margin-top: 0;
    }
    .goods-thumb {
        position: relative;
        flex: 0 0 7rem;
        width: 7rem;
        height: 7rem;
        margin-right: 0.6667rem;
        border-radius: 0.1667rem;
        background: rgba(0,0,0,0.03);
        &::before {
            content: '';
            position: absolute;
            left: 0;
            right: 0;
            top: 0;
            bottom: 0;
            z-index: 1;
            background: rgba(0, 0, 0, 0.03);
            border-radius: 0.1667rem;
        }
        .tag-presell {
            position: absolute;
            left: -0.3333rem;
            top: -0.3333rem;
            z-index: 2;
            height: 1.6667rem;
            padding: 0 0.6667rem;
            line-height: 1.6667rem;
            background: linear-gradient(180deg,rgba(255,118,36,1) 0%,rgba(246,44,0,1) 100%);
            box-shadow: 0 0.1333rem 0.2333rem 0 rgba(240,58,88,0.2);
            border-radius: 0.8333rem;
            font-size: 0.6667rem;
            color: #fff;
        }
        .thumb {
            width: 100%;
            height: 100%;
            vertical-align: top;
        }

    }

    .goods-info {
        position: relative;
        flex: 1 1 auto;
        padding-bottom: 1.6667rem;
        .title {
            max-height: 2.8rem;
            overflow: hidden;
            margin-bottom: 0.3333rem;
            line-height: 1.4rem;
            font-size: 0.9333rem;
            color: #222;
        }
        .infos {
            line-height: 0.7333rem;
            font-size: 0.7333rem;
            color: #888;
            .item {
                margin-bottom: 0.3333rem;
            }
        }
        .price{
            position: absolute;
            left: 0;
            bottom: 0;
            z-index: 9;
            line-height: 1.6667rem;
            font-size: 0.9333rem;
            color: #F03A58;
        }
        .buy-btn {
            position: absolute;
            right: 0;
            bottom: 0;
            z-index: 9;
            height: 1.6667rem;
            padding: 0 1rem;
            line-height: 1.6667rem;
            background: #D0021B;
            border-radius: 1.1667rem;
            font-size: 0.8rem;
            color: #fff;
            .icon {
                display: inline-block;
                width: 0.8rem;
                height: 1.1333rem;
                margin-top: -0.1333rem;
                margin-right: 0.1rem;
                vertical-align: middle;
                // background: url(./images/ico_flush.png) no-repeat center center;
                background-size: contain;
            }
        }
    }
}

.page-bottom {
  padding: 1.3333rem 0;
  text-align: center;
  font-size: 0.8rem;
  color: #c0c0c0;
}

.page-share-btn {
    position: fixed;
    bottom: 3.6667rem;
    right: 0.6667rem;
    z-index: 99;
    width: 3.3333rem;
    padding: 1.6667rem 0;
    background:#fff;
    box-shadow:0 1px 0.3667rem 0 rgba(0,0,0,0.1);
    border-radius: 1.6667rem;
    border:1px solid rgba(0,0,0,0.1);
    text-align: center;
    .icon {
        width: 1.6667rem;
        height: 1.6667rem;
        vertical-align: top;
    }
    .title {
        display: block;
        margin-top: 0.6667rem;
        line-height: 1rem;
        font-size: 0.8rem;
    }
}

.page-totop {
    position: fixed;
    right: 1rem;
    bottom: .5rem;
    z-index: 999;
    width: 2.67rem;
    height: 2.67rem;
    // background: url(officeImages/float_btn_scroll.png) no-repeat center center;
    background-size: contain;
    border-radius: 50%;
    opacity: 0.8;
}
</style>
