<template lang="html">
  <div class="sideWrap" :class="{'show':showing}">
    <div id="side" >
      <div class="chapter" style='margin:0;'>
          <router-link  class="link" to="/"> 首页 </router-link>
      </div>
      <div class="chapter" v-for="(item,index) in chapters" :key="item.title" v-if="item.title">
          <router-link  class="link" :to="genUrl(item.title)"> {{item.title}} </router-link>
      </div>


    </div>
    <div class="toogleSide"  @click="toogleSide"> {{showing?"<":">"}} </div>
  </div>
</template>

<script>
var arts = require('../../../../articles.json');
export default {
  data(){
    return {
      chapters:arts,
      showing: true
    }
  },
  methods:{
    toogleSide(){
      this.showing=!this.showing;
    },
    genUrl(url){
      return '/article/'+url;
    },
  }
}
</script>

<style lang="css" scoped>
a {
  text-decoration: none;
  color: #333;
}
.sideWrap{
  z-index:1;
  position: fixed;
  left: -12rem;
  top: 3rem;
  bottom: 3rem;
  width:12rem;
}
.toogleSide{
  z-index:1;
  width:3rem;
  height: 3rem;
  background-color: rgb(222, 222, 222);
  position: absolute;
  top:50%;
  right: -1.5rem;
  border-radius: 50%;
  font-size: 1.5rem;
  line-height: 3rem;
  color:rgb(255, 255, 255);
  text-align: right;
  padding:0.5rem;
  cursor: pointer;
}
.sideWrap.show{
  left: 0;
}
#side{
  position: absolute;
  z-index: 2;
  overflow: auto;
  background-color: #f3f3f3;
  width:12rem;
  height: 100%;
  border-right: 1px solid rgb(208, 208, 208);
  padding:2rem 0 ;
  padding-bottom: 5rem;
  box-sizing: border-box;
}
#side .chapter{
  width:100%;
  height:2.4rem;
  line-height: 2rem;
  padding: 0.2rem 2rem ;
  box-sizing: border-box;
}
#side .chapter .link{
  width:100%;
  display: block;
  text-decoration: none;
  color:#333;
  white-space: nowrap;
  text-overflow: ellipsis;
  overflow: hidden;
}
#side .chapter .link:hover{
  color: rgb(16, 122, 173);
  border-bottom: 1px solid rgb(16, 122, 173);
}
</style>
