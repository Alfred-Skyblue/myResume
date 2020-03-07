<template>
  <div :class="partFive">
    <h3 class="text-center text-top">工作经验</h3>
    <p>
      <a href="javascript:void(0)">河北万图计算机科技有限公司</a>
      <span class="text-small">| 2017/10 - 2019/12</span>
    </p>
    <p class="text-small">工作内容：<br>&emsp;本人主要负责公司外包项目的网页开发， 在工作中熟练使用JavaScript、Vue、HTML、CSS、jQuery，完成网页开发， 配合后台人员实现产品前端界面效果与功能。</p>
    <p class="text-small">日常操作：</p>
    <p class="text-small">&emsp;1. Vue + element-ui 编写后台页面、Vue + ECharts 报表制作……</p>
    <p class="text-small">&emsp;2. ECharts 报表汇总。使用 Vue + ECharts 进行报表设计，正在开发。</p>
  </div>
</template>

<script>
export default {
  name: "partFive",
  data() {
    return {
      partFive: "part-five",
      curWidth: 0
    };
  },
  beforeMount() {
    this.curWidth = document.documentElement.clientWidth || document.body.clientWidth;
    if(this.curWidth < 1600) {
      this.partFive = "part-five-responsive"
    }
  }
};
</script>

<style scoped>
a {
  color: deepskyblue;
}
a:hover {
  color: rgb(118, 190, 248);
}
.part-five {
  width: 100%;
  height: 310px;
  border: 40px solid transparent;
  border-image: url("~@/./assets/img/border_image.png") 30 30 stretch;
  background: #18202d;
}
.part-five-responsive {
  width: 100%;
  border: 40px solid transparent;
  border-image: url("~@/./assets/img/border_image.png") 30 30 stretch;
  background: #18202d;
}
.text-center {
  text-align: center;
}
.text-small {
  font-size: 0.9em;
  color: rgb(253, 239, 239);
}
</style>
