<template>
  <div class="cus-active">
    <div class="nav-wrapper fixed" v-show="scrollTop>top&& scrollTop!=0" >
    <ul class="nav-content">
      <li v-for="(item,index) in list" :key="index" class="nav-item">{{item.name}}</li>
    </ul>
  </div>
    <div class="scroll-wrapper" @scroll="scroll" ref="scrollWrapper">
      <div class="top-img" ref="topImg">
      <img :src="styleObj.topImg" alt="" class="top-img">
    </div>
    <div class="nav-wrapper" ref="nav">
      <ul class="nav-content">
        <li v-for="(item,index) in list" :key="index" class="nav-item">{{item.name}}</li>
      </ul>
    </div>
    <div class="floor-wrapper" :style="{background:styleObj.bgColor}">
      <div class="floor-item" v-for="(item,index) in list" :key="index">
        <div class="floor-title">{{item.name}}</div>
        <div class="goods-wrapper">
          <div v-for="(goods,i) in item.goodsList" :key="i">
            <div class="goods-item">{{goods.goodsName}}</div>
          </div>
        </div>
      </div>
    </div>
    </div>

  </div>
</template>

<script>
export default {
  data(){
    return{
      styleObj:{},
      list:[],
      top:0,
      scrollTop:0
    }
  },

  mounted(){
    window.addEventListener('scroll',this.scroll,true);
    },

  methods:{
    getInfo: function(){
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

      if(res.code == 0 && res.data){
              this.styleObj = res.data.style||{};
              this.list = res.data.list||[];
            }

            setTimeout(this.getFixHeight,100);


      // this.$nextTick(()=>{
      //   this.getFixHeight();
      // })
    },

    scroll: function(e){
      var scrollTop = e.target.documentElement.scrollTop || e.target.body.scrollTop;
      this.scrollTop = scrollTop;
      console.log(this.scrollTop)
    },

    getFixHeight: function(){
      var top = this.$refs.nav.offsetTop;
      this.top = top;
      console.log(this.top);
    }
  },

  created(){
this.getInfo()
  },

  destroyed(){
    window.removeEventListener('scroll', this.scroll)
  }

}
</script>

<style lang="css" scoped>
.cus-active{
  width:100vw;
  height:100vh;
}

.top-img{
  width: 100vw;
  display: block;
}
.nav-wrapper{
  background: #ffffff;
}

.nav-wrapper.fixed{
  position: fixed;
  top: 0;
  right: 0;
  left: 0;
}

.nav-content{
  overflow-y: hidden;
  overflow-x: auto;
  white-space: nowrap;
}

.nav-content .nav-item {
  display: inline-block;
  height: 2.67rem;
  line-height: 2.67rem;
  padding: 0 2rem;
}

.goods-item{
  width: 11.5rem;
  height: 21.33rem;
  background: #ffffff;
  display: inline-block;
  margin: 0 0.335rem;
}
</style>
