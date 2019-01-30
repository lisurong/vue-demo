<template>
	<div class="foodDetail">
  		{{foodData1.name}}
	</div>
</template>

<script>

export default {
  props:{
    foodData1:{
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
</style>
