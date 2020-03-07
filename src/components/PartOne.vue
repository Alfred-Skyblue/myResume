<template>
  <div class="part-one">
    <img class="part-one-image" :src="headImage" alt="头像">
    <p>姓&emsp;&emsp;名：杨攀腾</p>
    <p>学&emsp;&emsp;历：本科</p>
    <p>工作年限：2 年</p>
    <p>年&emsp;&emsp;龄：26</p>
    <p>联系电话：18631090554</p>
    <p>电子邮箱：893042011@qq.com</p>
    <p>博&emsp;&emsp;客：<a href="http://www.yptup.top/" target="_blank">yptup.top</a></p>
    <p>网&emsp;&emsp;站：<a href="http://my.yptup.top/" target="_blank">个人网站</a></p>
    <p>GitHub：<a href="https://github.com/Alfred-Skyblue" target="_blank">Alfred</a></p>
  </div>
</template>

<script>
export default {
  name: "partOne",
  data() {
    return {
      headImage: require('../assets/img/head_image.png')
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
p {
  line-height: 30px;
}
.part-one {
  width: 100%;
  height: 500px;
  border: 40px solid transparent;
  border-image: url("~@/./assets/img/border_image.png") 30 30 stretch;
  background: #18202d;
  padding-left: 10px;
}
.part-one-image {
  width: 150px;
  height: 150px;
}
</style>
