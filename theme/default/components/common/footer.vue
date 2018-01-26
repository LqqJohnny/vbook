<template lang="html">
<div>
    <div class="footer">
      {{bookinfo.author}} |  <a :href="footer.url">原网址</a>  | {{bookinfo.email}}
    </div>
</div>

</template>

<script>
import {bookinfo,footer} from '../../../../book.config.js'
export default {
  data(){
    return {
      footer: footer,
      bookinfo: bookinfo
    }
  },
}
</script>

<style lang="css" scoped>
.footer{
    z-index: 4;
    text-align: center;
    font-size:1rem;
    width:100%;
    height: 3rem;
    line-height: 3rem;
    background-color: #f3f3f3;
    box-shadow: 0px -1px 1px 1px #e6e6e6;
    color: rgb(115, 115, 115);
    padding:0 2rem;
    position: fixed;
    bottom: 0;
    left: 0;;
}

</style>
