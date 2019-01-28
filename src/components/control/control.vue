<template>
  <div>
    <span class="cz">
      <transition name="slide-fade"><em v-show="list.num" @click="jian($event)">-</em></transition><transition name="slide-fade"><i v-show="list.num">{{list.num}}</i></transition><em @click="add($event)">+</em>
    </span>
  </div>
</template>

<script>
import Vue from 'vue'

export default {
  props:{
   list:{
    type:Object
   }
  },
  data(){
    return{

    }
  },
  computed: {

  
  },
  methods:{
    add(event){
        if(!event._constructed){
          return;
        }else{
          if(!this.list.num){
            Vue.set(this.list, 'num', 1);
          }else{
            this.list.num++
          }
        }
      },
      jian(event){
        if(!event._constructed){
          return;
        }else{
          if(this.list.num<=0){
            return;
          }else{
            this.list.num--
          }
        }
      }
  }
}
</script>

<style scoped>
.cz{
  position: absolute;
  right: 10px;
  top:0;
}
.cz em{
  width: 20px;
  height: 20px;
  text-align: center;
  line-height: 20px;
  color: #fff;
  border-radius: 50%;
  display: inline-block;
  background: #11c9f5;
}
.slide-fade-enter-active {
  transition: all .3s ease;
}
.slide-fade-leave-active {
  transition: all .8s cubic-bezier(1.0, 0.5, 0.8, 1.0);
}
.slide-fade-enter, .slide-fade-leave-to
/* .slide-fade-leave-active for below version 2.1.8 */ {
  transform:translate3d(20px, 0px, 0px);
  opacity: 0;
}
</style>
