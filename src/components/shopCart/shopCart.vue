<template>
  <div>
    <div class="cart" >
      <div class="cartL" @click="showClick()">
        <div class="logo">
          <div class="cr"></div>
          <div class="num">{{totalNum}}</div>
        </div>
        <div class="price">￥{{totalPrice}}</div>
        <div class="ps">另需配送费：{{deliveryPrice}} 元</div>
      </div>
      <div class="cartR" :class="goPay">{{difference}}</div>    
    </div>
     <div class="cartContent" v-show="showF">
        <div class="cart-tit">
          <span class="tit-l">购物车</span>
          <span class="tit-r" @click="empty()">清空</span>
        <div class="cart-con" ref="aaa">
          <ul>
            <li v-for="item in selFood">
              <span>{{item.name}}</span>
              <control :list="item"></control>
            </li>
          </ul>
        </div>
        </div>
      </div>
      <div class="dig" v-show="showF" @click="showD()"></div>
  </div>
</template>

<script>
import control from '@/components/control/control'
import BScroll from 'better-scroll'

export default {
  components: {
      control
  },
  props:{
    minPrice:{
      type:Number
    },
    deliveryPrice:{
      type:Number
    },
    selFood:{
      type:Array,
      default:function(){
        return [
          {
            price:10,
            num:1
          }
        ]
        
      }
    }
  },
  data(){
    return{
      showFlag:false
    }
  },
  created() {
  },
  mounted () {
        this._initScrollCon()
  },
  computed: {
    showF:function(){
      let a;
      if(this.selFood.length){
        a = this.showFlag
      }
      return a;
    },
    //总价
    totalPrice:function(){
      let total = 0;
      for(let i=0;i<this.selFood.length;i++){
        let cur = this.selFood[i];
        total += cur.price*cur.num;
      }
      return total;
    },
    //总数量
    totalNum:function(){
      let num = 0;
      for(let i=0;i<this.selFood.length;i++){
        let cur = this.selFood[i];
        num += cur.num;
      }
      return num;
    },
    //差
    difference:function(){
      var diff = this.totalPrice-this.minPrice;
      if(diff>=0){
        return '去结算'
      }else{
        return '差'+Math.abs(diff)+'元起送'
      }
      
    },
    //去结算
    goPay:function(){
      var diff = this.totalPrice-this.minPrice;
      if(diff>=0){
        return 'goPay'
      }
    }
  },
  methods:{
    _initScrollCon:function(){
            this.aaa = new BScroll(this.$refs.aaa,{
                click: true
            });
      },
      showClick:function(){
        // console.log(this.totalNum)
        if(this.totalNum){
          this.showFlag = !this.showFlag;
        }
        
      },
      showD:function(){
        this.showFlag =false;
      },
      empty:function(){
        this.selFood.forEach((itme) => {
          itme.num = 0;
        })
        this.showFlag=false;
      }
  }
}
</script>

<style scoped>
.cart-con ul li{
  position: relative;
  margin: 15px 0;
}
.cart{
  position: fixed;
  bottom:0;
  left: 0;
  height: 50px;
  background: #58606d;
  width: 100%;
  display: flex;
  text-align: left;
  z-index: 101;
}
.logo{
    width: 50px;
    height: 50px;
    border-radius: 50%;
    background: #58606d;
    position: relative;
    top: -12px;
    padding-top: 5px;
    display: inline-block;
    vertical-align: middle;
    
}
.cartL{
  flex:1;
  color: #fff;
  font-size: 12px;
}
.cartR{
  flex: 0 0 100px;
  background: #8a8f96;
  color: #e1e2ec;
  line-height: 50px;
  text-align: left;
  padding-left: 10px;
}
.cartR.goPay{
  background: #3fb15e;
}
.cr{
    width: 50px;
    height: 50px;
    border-radius: 50%;
    background: #000;
    margin: 0 auto;

}
.num{
    position: absolute;
    width: 20px;
    height: 20px;
    color: #fff;
    background: #f00;
    top: 0px;
    right: 10px;
    border-radius: 50%;
    text-align: center;
    line-height: 20px;
}
.price{
  display: inline-block;
  margin-right: 5px;
  margin-left: 10px;
}
.ps{
  display: inline-block;
}
.dig{
    position: fixed;
    top: 0;
    left: 0;
    bottom: 0;
    right: 0;
    overflow: auto;
    z-index: 100;
    background: rgba(7,17,27,0.8);
    z-index: 10;
}
.cartContent{
  position: fixed;
  bottom:50px;
  left:0;
  width: 100%;
  z-index: 100;
  background: #fff;
}
.cart-con{
  height: 300px;
  overflow: hidden;
}
</style>
