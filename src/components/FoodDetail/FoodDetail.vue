<template>
	<div class="foodDetail">
    <div class="imgDiv">
      <img :src="foodData.image"/>
    </div>  
    <div class="content">
      <span>{{foodData.name}}</span>
      <div>
        <button>加入购物车</button>
        <control></control>
      </div>
    </div>		
	</div>
</template>

<script>
import control from '@/components/control/control'
export default {
  components: {
      control
  },
  props:{
    foodData:{
      type:Object
    }
  },
  data(){
      return{
        
  	}
  },
  methods:{
  
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.foodDetail{
  position: fixed;
  top: 0;
  left:0;
  bottom: 50px;
  background: #fff;
  width: 100%;
}
.imgDiv{
  width: 100%;
  height: 0;
  padding-top: 100%;
  position: relative;
}
.imgDiv img{
    position: absolute;
    top: 0;
    width: 100%;
    left: 0;
    height: 100%;
}
</style>
