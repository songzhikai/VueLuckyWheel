<template>
  <div>
      <ul class="lottery">
        <li id="0" class=""><img :src="prizes[0]"><div class="mask"></div></li>
        <li id="1" class=""><img :src="prizes[1]"><div class="mask"></div></li>
        <li id="2" class=""><img :src="prizes[2]"><div class="mask"></div></li>
        <li id="7" class=""><img :src="prizes[3]"><div class="mask"></div></li>
        <a href="javascript:void(0);" @click="startLottery" :style="'background-image:url('+prizes[8]+')'"></a>
        <li id="3" class=""><img :src="prizes[4]"><div class="mask"></div></li>
        <li id="6" class=""><img :src="prizes[5]"><div class="mask"></div></li>
        <li id="5" class=""><img :src="prizes[6]"><div class="mask"></div></li>
        <li id="4" class=""><img :src="prizes[7]"><div class="mask"></div></li>
      </ul>
  </div>
</template>
<script>
export default {
  data() {
    return {
      prizes: [
        require('../assets/lottery/1.jpg'), require('../assets/lottery/2.jpg'), require('../assets/lottery/3.jpg'), require('../assets/lottery/4.jpg'),
        require('../assets/lottery/5.jpg'), require('../assets/lottery/6.jpg'), require('../assets/lottery/7.jpg'), require('../assets/lottery/8.jpg'),
        require('../assets/lottery/9.jpg')],
      rollStepTimes: 1, //走的格子次数
      circleNum: 8, //每圈个数
      isPermStart: true, //开始抽奖标记
      timer: '', //定时器
      rollSpeed: 50, // 50毫秒走一个格子
      rollIndex: -1, //当前走到的格子 下标
      addOnCircles: 4, //空走4圈
      addOnCircles2: 6, //空走6圈
    };
  },
  created() {
  },
  computed: {
  },
  methods: {
    //开始抽奖
    startLottery(){
      //开始转从第二个开始
      // let lis = document.getElementsByTagName('li')
      // lis[0].className = 'active'
      if(this.isPermStart == true){
        this.isPermStart = false
        this.timer = setTimeout(this.rollCircle, this.rollSpeed)
      }
    },
    /**
     * 转圈
     * @param lis
     */
    rollCircle(){
      // console.log('11111111');
      this.rollIndex++
      this.rollStepTimes++
      if(this.rollIndex == 8){
        this.rollIndex = 0
      }
      for(let index=0;index<this.circleNum;index++){
        document.getElementsByTagName('li')[index].className = ''
        let idVal = document.getElementsByTagName('li')[index].id;
        if(idVal == this.rollIndex){
          document.getElementsByTagName('li')[index].className = 'active'
        }
      }
      //根据圈数改变速度
      if(this.rollStepTimes > this.addOnCircles*8){
        // console.log(this.rollSpeed);
        this.rollSpeed = 200
      }
      if(this.rollStepTimes > this.addOnCircles2*8){
        this.rollSpeed = 500
      }
      if(this.rollStepTimes == 7*8){ //7圈 停止
        this.initLottery();
        return;
      }
      this.timer = setTimeout(this.rollCircle, this.rollSpeed)
    },
    initLottery(){
      this.rollSpeed = 50
      this.isPermStart = true
      this.rollStepTimes = 1
      window.clearInterval(this.timer)
    }
  },
  mounted(){
  }
};
</script>
<style scoped>
  ul{border:4px solid #ba1809;width:570px;height:510px;margin:100px 400px;}
  li{position:relative;width:190px;height:170px;text-align:center;color:#333;font-index:-999;float:left}
  li img{display:block;width:190px;height:170px;}
  a{width:190px;height:170px;display:block;float:left;text-decoration:none;background:url(../assets/lottery/mask.jpg) no-repeat;}
  li.active .mask{display:block;}
  .mask{
    width:100%;
    height:100%;
    position:absolute;
    left:0;
    top:0;
    background-color: #adc092;
    background:url(../assets/lottery/mask.jpg) no-repeat;
    display:none;
  }
</style>

