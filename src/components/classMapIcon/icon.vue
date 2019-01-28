<template>
	<div>
    <span :class="classMap[type]"></span>
  </div>
</template>

<script>

export default {
  name: 'icon',
  created(){
    this.classMap=["className0","className1","className2","className3"]
  },
  data(){
      return{
        
  	}
  },
  methods:{
  
  },
  props: ['type']
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.className0{
  width: 15px;
  height: 15px;
  display: inline-block;
  background: #f00;
}
.className1{
  width: 15px;
  height: 15px;
  display: inline-block;
  background: #000;
}
.className2{
  width: 15px;
  height: 15px;
  display: inline-block;
  background: green;
}
.className3{
  width: 15px;
  height: 15px;
  display: inline-block;
  background: #999;
}
.className4{
  width: 15px;
  height: 15px;
  display: inline-block;
  background: #333;
}
</style>
