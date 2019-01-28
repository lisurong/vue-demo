<template>
  <div id="hello">
    <h1 @click='click()' v-bind:title="message"></h1>
    <h2 v-if="seen">Essential Links</h2>
    <input v-model='msg'/>
    <ul>
    	<todo v-bind:todoData='groceryList'></todo>
    </ul>
      <input type="checkbox" id="jack" value="Jack" v-model="checkedNames">
	  <label for="jack">Jack</label>
	  <input type="checkbox" id="john" value="John" v-model="checkedNames">
	  <label for="john">John</label>
	  <input type="checkbox" id="mike" value="Mike" v-model="checkedNames">
	  <label for="mike">Mike</label>
	  <br>
	  <span>Checked names: {{ checkedNames }}</span>
	  <br/>
	  <input type="radio" id="jack1" value="Jack1" v-model="picked">
	  <label for="jack1">Jack</label>
	  <input type="radio" id="john1" value="John1" v-model="picked">
	  <label for="john1">John</label>
	  <br/>
	  <span>Checked names: {{ picked }}</span>

	  <div>
	  	<textarea v-model="msg"></textarea>
	  </div>
	  <div>
	  	  <select v-model="selected">
			    <option disabled value="">请选择</option>
			    <option>A</option>
			    <option>B</option>
			    <option>C</option>
		  </select>
		  <span>Selected: {{ selected }}</span>
	  </div>
	  <div>
	  	<button @click="show=!show">点击我</button>
	  	<p v-if="show">hello</p>
	  </div>
	  <button  @click="get()">数据</button>
	  <div v-if="seller.supports">
	  	<!-- <span :class="classMap[seller.supports[0].type]"></span> -->
	  	<icon :type="seller.supports[0].type"></icon>
	  	<span>{{seller.supports[0].description}}</span>
	  </div>
	  <button>
	  	<router-link to="/goods">商品</router-link>
	  </button>
	  <button @click="showClick()">弹出层</button>
	  <div v-show="showDig" id="box">
		<div id="main" class="clearfix">
			<div id="content">
				<div class="main-star">
					<star :size="48" :mark="4.6"></star>
				</div>
				<div class="title">
					<div class="line"></div>
					<div class="text">双人套餐</div>
					<div class="line"></div>
				</div>
			</div>
		</div>
		<div id="footer">关闭</div>
	 </div>
	 <div class="fl">
	 	<div class="left"></div>
	 	<div class="right"></div>
	 </div>
  </div>
</template>

<script>

import todo from '@/components/todo'
import star from '@/components/star/star'
import icon from '@/components/classMapIcon/icon'

export default {
  name: 'HelloWorld',
  components: {
    todo,
    star,
    icon
  },
  created(){
  	this.classMap=["className0","className1","className2","className3"]
  },
  data(){
      return{
      	msg: 'Welcome to Your Vue.js App',
      	message: '页面加载于 ' + new Date().toLocaleString(),
      	seen:true,
      	show:true,
      	showDig:false,
        list:[],
        groceryList: [
	      { id: 0, text: '蔬菜' },
	      { id: 1, text: '奶酪' },
	      { id: 2, text: '随便其它什么人吃的东西' }
	    ],
	    checkedNames: [],
	    picked:'',
	    selected:'',
	    seller:{}
  	}
  },
  methods:{
  	click:function(){
  		this.msg='欢迎来到vue'
  	},
  	get:function(){
  		// let _this = this;
  		let params = {
  			type:'',
  			key:'5e23ff44f786ac31199f6b905991913a'
  		}
        this.$http.post('/api/toutiao/index',params,{emulateJSON:true}).then(function(res){
            // console.log(res.bodyText);
        	let result = JSON.parse(res.bodyText);
        	this.list = result.result.data;
        },function(){
            console.log('请求失败处理');   //失败处理
        });
    },
    showClick:function(){
    	this.showDig = true;
    }
  },
  mounted(){
  		this.get();
  		this.$http.get('/api/seller').then(function(res){

        	let result = JSON.parse(res.bodyText);
        	let data = result.data.seller;
        	this.seller = data;
        	// console.log(data);

        },function(){
            console.log('请求失败处理');   //失败处理
        });
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  margin: 0 10px;
}
a {
  color: #42b983;
}
.className{
	width: 15px;
	height: 15px;
	display: inline-block;
	background:green;
}

.main-star{
	margin: 20px 0;
}
.title{
	display: flex;
	width: 80%;
	margin: 0 auto;
}
.line{
	flex:1;
	border-bottom: 1px solid #f00;
	position: relative;
	top: -6px;
}
.text{
	font-size: 16px;
	font-weight: bold;
	color: #fff;
	padding: 0 15px;
}
.fl{
	position: absolute;
	top:530px;
	left: 0;
	right: 0;
	bottom:80px;
	display: flex;
	width: 100%;
	background: #fafafa;
}
.left{
	flex:0 0 80px;
	background: #666;
}
.right{ 	
	flex:1;
}
/**弹层**/
#box{position: fixed;top:0;left: 0;bottom: 0;right: 0;overflow: auto;z-index: 100;background: rgba(7,17,27,0.8);}
#main {min-height: 100%;color: #fff;font-size: 12px;width: 100%}  /* 必须使用和footer相同的高度 */
#content{padding-bottom: 150px; }
#footer {position: relative;margin-top: -150px; /* footer高度的负值 */height: 150px;clear:both;font-size: 24px;color: #fff;}
.clearfix:after {content: ".";display: block;height: 0;clear: both;visibility: hidden;}
.clearfix {display: inline-block;}
</style>
