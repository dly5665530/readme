<template>
  <div class="home">
    <van-search v-model="value" shape="round" background="#D43D3D" placeholder="请输入搜索关键词" @click="jinru"/>
    <van-tabs v-model="active" @click="toggle">
      <van-tab title="推荐"></van-tab>
      <van-tab title="视频"></van-tab>
      <van-tab title="热点"></van-tab>
      <van-tab title="社会"></van-tab>
      <van-tab title="娱乐"></van-tab>
      <van-tab title="军事"></van-tab>
      <van-tab title="科技"></van-tab>
      <van-tab title="汽车"></van-tab>
      <van-tab title="房产"></van-tab>
      <van-tab title="家居"></van-tab>
    </van-tabs>
    <div class="box" v-for="(item,index) in list" :key="index">
      <p>{{item.title}}</p>
      <!-- <div class="img" v-for="(url index) in "> -->
        <img :src="img | imges" alt="">
      <!-- </div> -->
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      active:"",
      value:"",
      img:"",
      list:[]
    };
  },
  methods: {
    onClickLeft() {
      Toast("返回");
    },
    onClickRight() {
      Toast("按钮");
    },
  },
  mounted() {
    this.$axios
      .get("http://api.kudesoft.cn/news/list", {
        params: {
          kw: "推荐",
        },
      }).then((res)=>{
        this.list=res.data.result.data
        this.img=res.data.result.data[name].imageUrls[0]
      })
  },
  methods:{
    toggle(name,title){
      console.log(name,title);
      this.$axios
      .get("http://api.kudesoft.cn/news/list", {
        params: {
          kw: title,
        },
      })
      .then((res) => {
        console.log(res);
        this.list=res.data.result.data
        this.img=res.data.result.data[name].imageUrls[0]
        console.log(this.img);
        // console.log(res.data.result.data[name].imageUrls[0]);
      });
    },
    jinru(){
      this.$router.push({path:"/about"})
    }
  },
  watch: {},
  filters:{
    imges(url){
      if(url.startsWith(" ")){
        return "https://ss2.bdstatic.com/70cFvnSh_Q1YnxGkpoWK1HF6hhy/it/u=1558026985,2729915815&fm=26&gp=0.jpg"
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