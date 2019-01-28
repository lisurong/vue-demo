<template>
	<div class="star" :class="'starType'">
  		<span class="star-item" v-for="(star,index) in stars" :class="star" :key = "index"></span>
	</div>
</template>

<script>
const LEN = 5;
const ON = "on";
const HARF = "harf";
const OFF = "off";
export default {
  name: 'star',
  props: {
      size:{
          type:Number
       },
      mark:{
        type:Number
      }
  },
  data(){
      return{
                
  	 }
  },
  computed:{
    starType:function(){
      return "star-"+this.size
    },
    stars:function(){
      let result = [];
      let score = Math.floor(this.mark*2)/2; //分数是0.5以下是整星1，0.5-0.9以上是半星，1.0 是整星2
      let harf = score%1 !==0; //如果不等于0，harf为true，说明是小数，代表是半星。如果等于0，harf为false, 说明是整数，代表整星
      for(var i=0;i<Math.floor(score);i++){ //先循环有几个整星
        result.push(ON);
      };
      if(harf){
         result.push(HARF);
      };
      // while(result.length<LEN){
      //   result.push(OFF);
      // }
      for(var i=result.length;i<LEN;i++){ //剩下的输出灰色的星星，从亮色的星星的长度开始循环，小于5的有几个，就输出几个灰色的
        result.push(OFF);
      };
      return result;
    }
  },
  methods:{
  
  }
 
}
</script>

<!-- Add "scopeda248
" attribute to limit CSS to this component only -->
<style scoped>
.star-48{}

.star-48 .star-item{
  display: inline-block;
  width: 20px;
  height: 20px;
  margin-right: 10px;
}

.star-48 .on{
  background: url(star48_on@2x.png) no-repeat;
  background-size: 100% 100%;
}
.star-48 .harf{
  background: url(star48_half@2x.png) no-repeat;
  background-size: 100% 100%;
}
.star-48 .off{
  background: url(star48_off@2x.png) no-repeat;
  background-size: 100% 100%
}
</style>
