<template>
  <div id="app">
    <Header></Header>
    <Side></Side>
    <Music v-if="musicOn" :src="musicSrc" :autoplay="autoplay" :loop="loop" :name="musicName"></Music>
    <div id="articlecontainer">
      <router-view :key="key"></router-view>
    </div>
    <Nav :key="key"></Nav>
    <div class="backImg" :style="styleObj"></div>
    <Footer></Footer>
  </div>
</template>

<script>
import Footer from "./components/common/footer.vue"
import Header from "./components/common/header.vue"
import Music from "./components/common/music.vue"
import Side from "./components/common/side.vue"
import Nav from "./components/common/nav.vue"
import 'normalize.css';
import {musicOn , musicSrc ,autoplay , musicLoop ,musicName} from './theme.config.js';

export default {
  name: 'app',
  data(){
    return {
      styleObj:{
        'backgroundImage':'url('+require('./src/bg.jpeg')+')'
      },
      musicOn: musicOn,
      autoplay: autoplay,
      musicSrc:musicSrc,
      loop: musicLoop,
      musicName:musicName
    }
  },
  components:{
    Header,Footer,Music,Side,Nav
  },
  computed: {
    key() {
        return this.$route.id !== undefined? this.$route.id + +new Date(): this.$route + +new Date()
    }
 }
}
</script>

<style>
#articlecontainer{
  z-index: 1;
  width:70%;
  margin: 5rem auto;
  border-radius: .5rem;
  padding: 0;
  overflow: hidden;


}
#articlecontainer img{
  max-width: 90%;
  display: block;
  margin:0 auto;

}
.backImg{
  z-index: -1;
  background-position: 60% 80%;
  position: fixed;
  width:12rem;
  height:17rem;
  right:0;
  top:66%;
  background-repeat: no-repeat;
  background-size: 100% 100%;
  opacity: 0.3;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
.articleInfo img{
  box-shadow: 0px 0px 10px 3px #000000;
  display: block;
  margin: 3rem auto;
  max-width:40%;
}

.articleInfo img:visited{
  width:100%;
}

.clearfix{zoom:1}
.clearfix:after{
     content:".";
     display:block;
     height:0;
     clear:both;
     visibility:hidden;

}
li{
  list-style: none;
}
@media only screen and (max-width: 641px){
  #articlecontainer{
    width: 100%;
  }
}
</style>
