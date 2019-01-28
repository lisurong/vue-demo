<template>
  <div class="food">
      <div class="fl">
        <div class="left" ref="left">
          <ul>
            <li v-for="(item, index) in goods" :class="{'current': currentIndex === index}" @click="selectItem(index, $event)">
              {{item.name}}
            </li>
          </ul>
        </div>
        <div class="right" ref="right">
          <ul>
             <li v-for="(item,index) in goods"  class="food"> 
                <strong>{{item.name}}</strong>
                <ul>
                    <li v-for="list in item.foods">
                      {{list.name}}<span class="price">{{list.price}}</span>
                      <control :list="list"></control>
                    </li>
                </ul>
            </li> 
          </ul>
        </div>
     </div>
     <shopCart :deliveryPrice="seller.deliveryPrice" :minPrice="seller.minPrice" :selFood="selFood"></shopCart>
  </div>
</template>

<script>
import shopCart from '@/components/shopCart/shopCart'
import control from '@/components/control/control'
import BScroll from 'better-scroll'

export default {
  components: {
      shopCart,
      control
  },
  data(){
      return{
       goods:[],
       listHeight: [],
       scrollY: 0,
       seller:{}
  	}
  },
  created() {
      this.$http.get('/api/goods').then(function(res){

          let result = JSON.parse(res.bodyText);
          let data = result.data.goods;
          this.goods = data;
          this.$nextTick(()=>{
              this._initScroll();
              this._getHeight();
          })

        },function(){
            console.log('请求失败处理');   //失败处理
        });
      this.$http.get('/api/seller').then(function(res){

          let result = JSON.parse(res.bodyText);
          let data = result.data.seller;
          this.seller = data;
          

        },function(){
            console.log('请求失败处理');   //失败处理
        });
  },
  computed:{
     currentIndex(){
        for(let i = 0;i<this.listHeight.length;i++){
          let height1 = this.listHeight[i];
          let height2 = this.listHeight[i+1];
          if(!height2 || (this.scrollY>=height1 && this.scrollY<height2)){
            return i;
          }
        }
        return 0;
     },
     selFood(){
        let foods = [];
        this.goods.forEach((good) => {
          good.foods.forEach((food) => {
            if(food.num){
              foods.push(food);
             }
             
         }); 
                    
       }); 
        return foods;
     }
  },
  methods:{
      selectItem(index,event){
        if(!event._constructed){
          return;
        }else{
          let FoodList = this.$refs.right.getElementsByClassName("food");
          let item = FoodList[index];
          this.right.scrollToElement(item,300);
        }
      },
      _initScroll () {
            this.left = new BScroll(this.$refs.left,{
                click: true
            });
            this.right = new BScroll(this.$refs.right,{
                click: true,
                probeType: 3
            });
            this.right.on('scroll', (pos) => {
                this.scrollY = Math.abs(Math.round(pos.y));
            })
      },
      _getHeight(){
        let FoodList = this.$refs.right.getElementsByClassName("food");
        let height = 0;
        this.listHeight.push(height);
        for(let i=0;i<FoodList.length;i++){
          height += FoodList[i].clientHeight;
          this.listHeight.push(height);
        }
      }
      
  
  },
   mounted(){
        
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
ul{
  padding: 0
}
li{
  list-style: none;
  margin: 15px 0;
  position: relative;
}
.fl{
  position: absolute;
  top:0;
  left: 0;
  right: 0;
  bottom:50px;
  display: flex;
  width: 100%;
  overflow: hidden;
  background: #fafafa;
}
.left{
  flex:0 0 80px;
  background: #f3f3f3;
}
.left .current{
  background: #fff;
}
.right{   
  flex:1;
}
.right li:last-child{

}
strong{
  background: #999;
  height: 30px;
  color: #fff;
  width: 100%;
  padding: 5px 15px;
  text-align: left;
  display: block;
}
.price{
  color: #f00;
}

</style>
