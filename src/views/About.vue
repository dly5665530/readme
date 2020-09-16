<template>
  <div class="about">
    <van-search
      v-model="value"
      shape="round"
      background="#D43D3D"
      placeholder="请输入搜索内容"
      @keydown.enter="sousuo"
    />

    <h3>
      历史记录
      <van-icon name="delete" @click="remove"/>
    </h3>
    <div class="history">
      <span  v-for="(item,index) in history" :key="index">{{item}}</span>
    </div>
    <h3>猜你想搜</h3>
  </div>
</template>
<script>
export default {
  data() {
    return {
      value: "",
      history: [],
    };
  },
  mounted() {
    // localStorage.getItem("history")
    let history = localStorage.history;
    if (history) {
      this.history = JSON.parse(history);
    }
  },
  methods: {
    sousuo() {
      this.history.unshift(this.value);
      localStorage.history = JSON.stringify(this.history);
      this.$router.push({ path: "/sousuo", query: { value: this.value } });
    },
    remove(){
      localStorage.removeItem("history")
      this.history=[]
    }
  },
};
</script>

<style lang="scss" scoped>
h3 {
  font-weight: 300;
  color: #ccc;
  display: flex;
  justify-content: space-between;
  box-sizing: border-box;
  padding: 10px;
}
.history {
  width: 100%;
  height: 70px;
}
span{
  margin-left: 10px;
}
</style>
