<template lang="html">
<div class="nav" v-if="id">
  <div class="navitem prev" @click="prevChapter">上一章</div>
  <div class="navitem next" @click="nextChapter">下一章</div>
</div>
</template>

<script>
import arts from '../../../../articles.json';
export default {
  data(){
    return {
    }
  },
  computed:{
    id(){
      var id = this.$router.history.current.params.id;
      return id;
    }
  },
  methods:{
  //  获取当前章节的 index
    getIdx(){
      var id = this.id;
      var idx = -1;
      for(var i = 0 ;i<arts.length; i++){
        var val = arts[i];
        if(val.title && val.title===id){
          idx = val.index;
          break;
        }
      }
      return idx;
    },
    // 点击下一章
    nextChapter(){
      var index = parseInt(this.getIdx());
      if(index === arts.length-1){
        alert("已经是最后一张了！");
        return ;
      }
      var nextId = arts[index+1].title;
      this.$router.push({ path: '/article/'+nextId});
    },
    // 点击上一章
    prevChapter(){
      var index = parseInt(this.getIdx());
      if(index===1){
        this.$router.push({ path: '/'});
        return ;
      }

      var nextId = arts[index-1].title;
      this.$router.push({ path: '/article/'+nextId});
    }
  }
}
</script>

<style lang="css" scoped>
.nav{
  position: fixed;
  right: 3rem;
  top: 5rem;

}
.nav .navitem{
  padding:0.3rem 1rem;
  background-color: rgb(244, 244, 244);
  border: 1px solid rgb(164, 164, 164);
  border-radius: 0.3rem;
  cursor: pointer;
  display: inline-block;
}
.nav .navitem:hover{
  background-color: #4AAFE3;
  color:#fff;
  border-color: #4AAFE3;
}
@media only screen and (max-width: 641px){
  .nav{
    right:2rem;
    top: 4rem;
  }
}
</style>
