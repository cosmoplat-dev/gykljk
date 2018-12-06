<template>
  <div class="home">
    <p class="sight">
      <img src="/xmountain.jpeg" >
      <span class="circles" v-for="(item,index) in sights" :key="index" :style="item.style" :title="item.sightname" :class="(item.people>=500)?'crowd':(item.people<300)?'unblocked':'limited'"></span>
      <ul class="circle-list">
        <li><p>流量正常</p> <span></span> </li>
        <li><p>流量达到门限</p> <span></span></li>
        <li><p>流量警告</p> <span></span></li>
      </ul>
    </p>
    <div class="weather">
      <!-- <iframe id="fancybox-frame" name="fancybox-frame1536824890031" frameborder="0" scrolling="no" hspace="0"  src="http://i.tianqi.com/index.php?c=code&a=getcode&id=40&h=25&w=310"></iframe> -->
     <!-- <iframe name="weather_inc" src="http://i.tianqi.com/index.php?c=code&id=55&py=haidian" width="255" height="184" frameborder="0" marginwidth="0" marginheight="0" scrolling="no"></iframe> -->
     <!-- <iframe id="fancybox-frame" name="fancybox-frame1536824492024" frameborder="0" scrolling="no" hspace="0"  src="http://i.tianqi.com/index.php?c=code&a=getcode&id=34&h=25&w=280"></iframe>   -->
    </div>
  </div>
</template>

<script>
sight=[{sightname:'香炉峰',style:'left:18px; top:243px;',people:1230,num:31},
        {sightname:'西山晴雪',style:'top: 219px; left:221px;',people:234,num:29},
        {sightname:'梯云山馆',style:'top: 190px; left: 330px;',people:226,num:23},
        {sightname:'玉华四院',style:'top: 212px; left: 383px;',people:356,num:22},
        {sightname:'朝阳湖',style:'top: 317px; left: 174px;',people:100,num:30},
        {sightname:'栖月山庄',style:'top: 296px; left: 291px;',people:234,num:28},
        {sightname:'森玉芴',style:'top: 337px; left: 268px;',people:345,num:29},
        {sightname:'玉华三院',style:'top: 253px; left: 376px;',people:678,num:24},
        {sightname:'多景亭',style:'top: 293px; left: 364px;',people:11,num:25},
        {sightname:'阆风亭',style:'top: 333px;left: 412px;',people:55,num:26},
        {sightname:'玉香馆',style:'top: 403px;left: 421px;',people:665,num:27},
        {sightname:'白松亭',style:'top: 398px;left: 492px;',people:221,num:16},
        {sightname:'香山寺遗址',style:'top: 424px; left: 506px;',people:334,num:15},
        {sightname:'双清',style:'top: 443px; left: 599px;',people:456,num:13},
        {sightname:'看云起',style:'top: 469px;left: 610px;',people:432,num:14},
        {sightname:'半山亭',style:'top: 373px;left: 576px;',people:200,num:12},
        {sightname:'观音阁',style:'top: 194px; left: 409px;',people:137,num:21},
        {sightname:'芙蓉馆',style:'top: 224px;left: 449px;',people:246,num:20},
        {sightname:'玉华山庄',style:'top: 280px;left: 449px;',people:567,num:19},
        {sightname:'多云亭',style:'top: 273px;left: 549px;',people:334,num:10},
        {sightname:'十八盘',style:'top: 320px;left: 523px;',people:111,num:18},
        {sightname:'洪光寺',style:'top: 356px;left: 523px;',people:222,num:17},
        {sightname:'香山饭店',style:'top: 318px; left: 565px;',people:256,num:11},
        {sightname:'望峰亭',style:'top: 235px;left: 556px;',people:231,num:8},
        {sightname:'松林餐厅',style:'top: 189px;left: 539px;',people:33,num:7},
        {sightname:'琉璃塔',style:'top: 186px;left: 485px;',people:68,num:9},
        {sightname:'昭庙',style:'top: 164px; left: 508px;;',people:99,num:6},
        {sightname:'见心斋',style:'top: 114px;left: 480px;',people:257,num:2},
        {sightname:'觐憩',style:'top: 129px; left: 536px;',people:112,num:5},
        {sightname:'香山别墅',style:'top: 153px;left: 576px;',people:99,num:3},
        {sightname:'东门',style:'top: 248px;left: 635px;',people:600,num:4},
        {sightname:'下站',style:'top: 53px;left: 525px;',people:289,num:1}]



function emulateTour(){
  for(var i =0; i<sight.length; i++){
      var num = Math.random()*15;
      var addOrReduce = Math.random()*10>5?1:-1;
      if(sight[i].people < 500){
          sight[i].people += addOrReduce * num;
      } else {
          sight[i].people -= num;
      }
    }
}
//
export default {
  data () {
    return {
      sights:sight
    }
  },
  mounted(){
    var timer = setInterval(emulateTour,5000);
  },
  methods: {
  },
}
</script>


<style lang="less" scoped>
.home {
  text-align: center;
}

.sight{
  position: relative;
}

.home .limited{
  border: 1px solid #bdb00f;
  background: yellow;
  box-shadow: 1px 1px 5px 2px #cece22;
}
.home .unblocked{
  background: #5cff5c;
  border: 1px solid #499232;
  box-shadow: 0px 0px 4px 2px #388810;
}
.home .crowd{
  border: 1px solid #b90101;
  background: red;
  box-shadow: -1px 1px 10px 1px #9a1036;
}

.circles {
  position:absolute;
  top:0;
  left: 0;
  width:10px;
  height: 10px;
  border-radius: 50%;
  border: 1px solid #499232;
  background: #5cff5c;
  cursor: pointer;
}
.circle-list {
  padding: 0;
  margin: 0 auto;
  overflow: hidden;
  list-style: none;
}
.circle-list li{
  margin: 0 1rem;
  display: inline-block;
  text-align: center;
}
.circle-list li span{
  display:inline-block;
  width:30px;
  height: 30px;
  border: 1px solid #499232;
  background: #5cff5c;
  border-radius: 50%;
  text-align: center;
}
.circle-list li:nth-child(2) span{
  border: 1px solid #bdb00f;
  background: yellow;
}
.circle-list li:nth-child(3) span{
  border: 1px solid #b90101;
  background: red;
}
.weather{
  position:absolute;
  top:15px;
  left:52px;
}
</style>
