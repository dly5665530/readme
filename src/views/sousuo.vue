<template>
  <div>
      <van-search v-model="value" shape="round" background="#D43D3D" :placeholder="keywords"/>
    <div class="box" v-for="(item,index) in list" :key="index">
      <p>{{item.title}}</p>
      <img :src="img | imges" alt />
      
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
        keywords:this.$route.query.value,
        list:[],
        img:"",
        value:this.keywords
    };
  },
  mounted(){
      this.$axios.get("http://api.kudesoft.cn/news/list",{
        params:{
          kw:this.keywords
        }
      }).then((res)=>{
        console.log(res);
        this.list=res.data.result.data
        this.img=res.data.result.data[0].imageUrls[0]
      })
  },
  filters:{
    imges(url){
      if(url.startsWith(" ")){
        return "http://p6-tt-ipv6.byteimg.com/img/tos-cn-i-0004/1075f7ff71be4e2280dcc13a69f808c2~tplv-tt-cs0:640:360.jpg"
      }else{
        return url
      }
    }
  }
};
</script>

<style lang="scss" scoped>
.box{
  width: 100%;
  display: flex;
  align-items: center;
  height: 80px;
  justify-content: space-around;
  img{
    width: 100px;
  }
}
</style>