<template>
	<div>
  		<li v-for="item in todoData">{{item.text}}</li>
	</div>
</template>

<script>

export default {
  name: 'todo',
  data(){
      return{
        
  	}
  },
  methods:{
  
  },
  props: ['todoData']
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
