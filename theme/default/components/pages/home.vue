<template lang="html">
<div class="home">
    <vue-lazy-component
      class="lazyComponent"
      :class="{'done' : slideStart}"
      :timeout='500'
      @after-enter="afterInit">
      <div class="bookInfo" v-html="homePage">
      </div>
      <artListSkt slot="skeleton"/>
    </vue-lazy-component>
    <div style="text-align:center;"><router-link :to="firstPage" class="start">开始阅读</router-link></div>
</div>
</template>

<script>
var arts = require('../../../../articles.json');
const homePage = require('../../../../articles/home.md');
import {bookinfo} from '../../../../book.config.js'
import artListSkt from '../common/artListSkt.vue'
export default {
  data(){
    return {
      homePage:homePage,
      slideStart: false
    }
  },
  computed:{
    firstPage(){
      var title = arts[1].title;
      return '/article/'+title;
    }
  },
  components:{
      artListSkt
  },
  mounted(){
      document.title= bookinfo.title ;
  },
  methods:{
    afterInit(){
      this.slideStart = true;
      console.log(this.slideStart);
    },
    genUrl(name){
      return "/article/"+name.replace(/\.md/g,'');
    },
    genTitle(name){
      return name.replace(/\.md/g,'');
    },
    getDate(time){
      var date = new Date(time);
      return date.getFullYear()+" / "+(date.getMonth()+1)+" / "+date.getDate();
    },
    search(){
      var query = this.searchword;
      if(query===""){
        this.list = arts;
      }else{
        this.list = arts.filter(function(val){
          return val.title.indexOf(query)>=0;
        })
      }
    }
  }
}
</script>

<style lang="css" scoped>
.start{
  height:2rem;
  color:#fff;
  background-color: rgb(67, 119, 187);
  border-radius: .5rem;
  padding:0.2rem 1rem;
  line-height: 2rem;
  text-decoration: none;
  display: inline-block;
  text-align: center;
}
.home{
  position: relative;
}
.title{
  font-size: 1rem;
  background-image: linear-gradient(to bottom,#f5f5f5 0,#e8e8e8 100%);
  background-repeat: repeat-x;
  padding:0.5rem 1rem;
}
.article_item{
  border-bottom: 1px solid #e0e0e0;
  padding: 0.8rem 2rem ;
}
.article_item a{
  text-decoration: none;
  color: #428bca;
  padding:.3rem;
}
.article_item a:hover{
  border-bottom: 2px solid rgb(18, 149, 244);
  color: #1693ff;
}
.article_item .date{
  float: right;
  color: rgb(115, 115, 115);
}
.searchFrame{
  position: absolute;
  top: 0.2rem;
  right:2rem;
  width:6rem;
  height:1.6rem;

}
.bookInfo{
  padding: 0 0.2rem;
}
.searchFrame .searchBar{
  display: inline-block;
  width: 100%;
  height:100%;
  padding:0 .5rem;
  border-radius: 1rem;
  border:1px solid rgb(198, 198, 198);
  font-size: .8rem;
  background-color: #fff;
  box-sizing:content-box;
}
.searchFrame .icon{
  position: absolute;
  display: block;
  width:1rem;
  height: 1rem;
  right:-0.2rem;
  top:0.3rem;
  background: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABAAAAAQCAYAAAAf8/9hAAABmklEQVQ4T4VTwXHCMBC8NaBvSAdOBSEdQAXQQUgFMQ+k4ZcfI/Gw0wElkA5MBaGDpIPkbca6zHkkYpyE+OeTtLu3ewfqfHmeD6uqmiZJksYjZn7RWh+6d+Uf7aK19gnAIzMDQPOAmYcAbomoJKJFF+gE4JwrmXkEINNab9vA6/U67fV6UhOgSRukAXDOFcw8BzAOrJkxZt6VbK3dApjWdX23Wq3emxYC+huAiRS894X3fhYvdEGcc+/MXEYCBPaxMWZkrT0opcaLxeLzN8OCWlGWa62vGwXSOxEdtNaZJHDpsTyQO8fj8UMUL5fLsgEIkp7+Yo118UCkO+ckpm+AqOASQPCqGAwG8zMFkj0R3Rtjbi4BiFcAdsycMnNhjBmepUBED938W9KFJFVKZVVVvRLR/pRCnANR0R6SYJYwCpP0XogHRDRTSqXR7NMkxiEBUPT7/ed2GpvNZszMORGNiEgiPk3jj10gogzAVZh92YUUgCzWvq7reZIksi/TCHIG0Op5Ftik9Om937UnM6oVkF8B/psHOQ9+HL4AMYHp6sjRRpAAAAAASUVORK5CYII=);
}
.searchFrame .searchBar:focus{
      outline: none;
}
:-moz-placeholder { /* Mozilla Firefox 4 to 18 */
    color: #b9b5b5; opacity:1;
}

::-moz-placeholder { /* Mozilla Firefox 19+ */
    color: #b9b5b5;opacity:1;
}

input:-ms-input-placeholder{
    color: #b9b5b5;opacity:1;
}

input::-webkit-input-placeholder{
    color: #b9b5b5;opacity:1;
}
.lazyComponent{
  max-height: 11rem;
  min-height: 11rem;
  overflow: hidden;
  transition: max-height ease 5s;
}

.lazyComponent.done{
  max-height:10000vh;
  min-height: 0;
  transition: max-height ease-in 5s;
}

</style>
