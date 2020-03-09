ECharts 打造个人线上简历


# 使用方法

* 安装依赖：npm install
* 开发模式：npm run dev
* 打包模式：npm run build

## 项目描述
项目描述，本项目是用vue+ECharts打造的个人简历页面

话不多说，先上代码
```js
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
```

上面是个人信息填充

## 好友分布

```js
<template>
  <div class="part-two" id="part-two"></div>
</template>

<script>
// 引入基本模板
let echarts = require("echarts/lib/echarts");

// 引用中国地图
require("echarts/map/js/china.js");

export default {
  name: "partTwo",
  data() {
    return {};
  },
  mounted() {
    this.drawECharts();
  },
  methods: {
    drawECharts() {
      // 基于准备好的dom，初始化echarts实例
      let myChart = echarts.init(document.getElementById("part-two"));

      // 排行前五城市
      let myFirendCity = [
        { name: "广州", value: ["113.23", "23.16", "2"] },
        { name: "深圳", value: ["114.07", "22.62", "3"] },
        { name: "上海", value: ["121.48", "31.22", "6"] },
        { name: "郑州", value: ["112.42", "34.43", "16"] },
        { name: "北京", value: ["116.46", "39.92", "2"] },
        { name: "邯郸", value: ["114.40", "36.40", "12"] }
      ];

      // 好友分布省份
      let myFriendProvince = [
        { name: "北京", value: 2 },
        { name: "上海", value: 6 },
        { name: "河北", value: 12 },
        { name: "河南", value: 16 },
        { name: "广州", value: 2 },
        { name: "深圳", value: 3 },
        { name: "广东", value: 5 }
      ];

      myChart.setOption({
        // 标题
        title: {
          text: "前端好友分布",
          textStyle: {
            color: "#fff"
          },
          subtext: "微信统计",
          subtextStyle: {
            color: "#fff"
          },
          x: "center"
        },
        // 移动显示
        tooltip: {
          trigger: "item",
          // 鼠标移动过去显示
          formatter: function(params) {
            if (!params.value[2]) {
              if (params.name && !isNaN(params.value)) {
                return params.name + " : " + params.value;
              } else {
                return "该地区暂无好友";
              }
            } else {
              return params.name + " : " + params.value[2];
            }
          }
        },
        // 左边注记
        visualMap: {
          text: ["", "好友数"],
          min: 0,
          max: 30,
          // 是否能通过手柄显示
          calculable: true,
          inRange: {
            color: ["#e4e004", "#ff5506", "#ff0000"]
          },
          textStyle: {
            color: "#fff"
          }
        },
        // geo
        geo: {
          map: "china"
        },
        // 数据
        series: [
          // 排行前五城市
          {
            name: "排行前五",
            type: "effectScatter",
            coordinateSystem: "geo",
            symbolSize: function(val) {
              return val[2] * 2;
            },
            showEffectOn: "render",
            rippleEffect: {
              brushType: "stroke"
            },
            hoverAnimation: true,
            label: {
              normal: {
                formatter: "{b}",
                position: "right",
                show: true,
                color: "#fff"
              }
            },
            itemStyle: {
              normal: {
                color: "#ddb926",
                shadowBlur: 10,
                shadowColor: "#333"
              }
            },
            // 类似于 z-index
            zlevel: 1,
            data: myFirendCity
          },
          // 好友分布省份
          {
            name: "好友数",
            type: "map",
            mapType: "china",
            // 是否允许缩放
            roam: false,
            label: {
              // 显示省份标签
              normal: {
                formatter: myFirendCity,
                show: false,
                textStyle: {
                  color: "#fff"
                }
              },
              // 对应的鼠标悬浮效果
              emphasis: {
                show: false
              }
            },
            itemStyle: {
              normal: {
                borderWidth: 0.5, // 区域边框宽度
                borderColor: "#fff", // 区域边框颜色
                areaColor: "deepskyblue" // 区域颜色
              },
              // 对应的鼠标悬浮效果
              emphasis: {
                borderWidth: 1,
                borderColor: "#fff",
                areaColor: "#00aeff"
              }
            },
            // 数据
            data: myFriendProvince
          }
        ]
      });
    }
  }
};
</script>

<style scoped>
.part-two {
  width: 100%;
  height: 500px;
  border: 40px solid transparent;
  border-image: url("~@/./assets/img/border_image.png") 30 30 stretch;
  background: #18202d;
}
</style>
```

+	首先，引用了 ECharts 及它的中国地图：

```js
let echarts = require("echarts/lib/echarts");

require("echarts/map/js/china.js");
```

+	然后，初始化 DOM 和数据：

```js
let myChart = echarts.init(document.getElementById("part-two"));

  // 排行前五城市
  let myFirendCity = [
	{ name: "广州", value: ["113.23", "23.16", "2"] },
	{ name: "深圳", value: ["114.07", "22.62", "3"] },
	{ name: "上海", value: ["121.48", "31.22", "6"] },
	{ name: "郑州", value: ["112.42", "34.43", "16"] },
	{ name: "北京", value: ["116.46", "39.92", "2"] },
	{ name: "邯郸", value: ["114.40", "36.40", "12"] }
  ];

  // 好友分布省份
  let myFriendProvince = [
	{ name: "北京", value: 2 },
	{ name: "上海", value: 6 },
	{ name: "河北", value: 12 },
	{ name: "河南", value: 16 },
	{ name: "广州", value: 2 },
	{ name: "深圳", value: 3 },
	{ name: "广东", value: 5 }
  ];
```

+	最后，我们通过 setOption 实现了地图的描绘，上面配置仅是个人配置方法，详细的方法请参考：[ECharts 配置](https://www.echartsjs.com/zh/option.html#title)。

## 技能特长
+	说到简历，还记得之前看过一份，印象特深，因为人家就是用 Word 中用图表展示的。所以，咱也试试：

```js
<template>
  <div :class="partThree" id="part-three"></div>
</template>

<script>

// 引入基本模板
let echarts = require("echarts/lib/echarts");

export default {
  name: "partThree",
  data() {
    return {
      partThree: "part-three",
      curWidth: 0,
      clear: null
    };
  },
  beforeMount() {
    this.curWidth = document.documentElement.clientWidth || document.body.clientWidth;
    if(this.curWidth < 1600) {
      this.partThree = "part-three-responsive"
    }
  },
  mounted() {
    this.clear=this.drawECharts();
  },
  methods: {
    drawECharts() {
      // 基于准备好的dom，初始化echarts实例
      let myChart = echarts.init(document.getElementById("part-three"));

      myChart.setOption({
        // 标题
        title: {
          // 标题文本
          text: "技能分布图",
          // 标题样式
          textStyle: {
            color: "#fff"
          },
          // 标题位置
          x: "center"
        },
        // 移动显示
        tooltip: {
          trigger: "item",
          // 显示文字样式
          formatter: "{a} <br/>{b} : {d}%"
        },
        // 注记
        legend: {
          x: "center",
          y: "bottom",
          textStyle: {
            color: "#fff"
          },
          data: [ "HTML5", "CSS3", "JavaScript", "jQuery", "Vue", "Node", "微信小程序", "其他" ]
        },
        // 注记显示手柄
        calculable: true,
        // 图形系列
        series: [
          {
            name: "技能分布",
            type: "pie",
            radius: [30, 110],
            roseType: "area",
            data: [
              { value: 15, name: "HTML5" },
              { value: 15, name: "CSS3" },
              { value: 20, name: "JavaScript" },
              { value: 20, name: "jQuery" },
              { value: 20, name: "Vue" },

            ]
          }
        ],
        // 颜色调整
        color: ['#00bfff', '#00ffdd', '#207ffc', '#00aeff', "#00eeff", "#006eff", "#0099ff", "#0066ff"]
      });

      return myChart
    }
  },
  beforeDestroy () {

   this.clear.clear()
  },
};
</script>

<style scoped>
.part-three {
  width: 100%;
  height: 500px;
  border: 40px solid transparent;
  border-image: url("~@/./assets/img/border_image.png") 30 30 stretch;
  background: #18202d;
}
.part-three-responsive {
  width: 100%;
  height: 500px;
  border: 10px solid transparent;
  border-image: url("~@/./assets/img/border_image.png") 30 30 stretch;
  background: #18202d;
}
</style>
```

## 个人博客文章图标
有时候就是想偷懒，也想不起自己还有啥好吹的了，于是贴个自己的个人博客文章吧：

>PartFour.vue

```js
<template>
  <div :class="partFour" id="part-four"></div>
</template>

<script>
// 引入基本模板
let echarts = require("echarts/lib/echarts");

export default {
  name: "partFour",
  data() {
    return {
      partFour: "part-four",
      curWidth: 0
    };
  },
  beforeMount() {
    this.curWidth = document.documentElement.clientWidth || document.body.clientWidth;
    if(this.curWidth < 1600) {
      this.partFour = "part-four-responsive"
    }
  },
  mounted() {
    this.drawECharts();
  },
  methods: {
    drawECharts() {
      // 基于准备好的dom，初始化echarts实例
      let myChart = echarts.init(document.getElementById("part-four"));

      myChart.setOption({
        // 标题
        title: {
          // 标题文本
          text: "文章成就统计",
          // 标题文本样式
          textStyle: {
            color: "#fff"
          },
          // 标题位置
          x: "center"
        },
        // 图形布局
        grid: {
          // 距离底部高度
          bottom: "20"
        },
        // 横轴
        xAxis: {
          show: false,
          type: "category",
          data: ["博客文章 \n 数量：53", "个人网站：\n3个"],
          axisLine: {
            lineStyle: {
              color: "#fff"
            }
          },
          axisLabel: {
            // 横轴信息全部显示
            interval: 0
          }
        },
        // 纵轴
        yAxis: {
          type: "value",
          axisLine: {
            lineStyle: {
              color: "#fff"
            }
          },
          axisLabel: {
            // 横轴信息全部显示
            interval: 0
          }
        },
        // 图形系列
        series: [
          {
            // 图类型
            type: "bar",
            // 数据
            data: [1141, 269, 1508, 234],
            // 文本
            label: {
              show: true,
              position: "top",
              color: "#fff",
              formatter: "{b}"
            },
            // 柱条样式
            itemStyle: {
              color: "deepskyblue"
            },
            zlevel: 1
          }
        ]
      });
    }
  }
};
</script>

<style scoped>
.part-four {
  width: 100%;
  height: 310px;
  border: 40px solid transparent;
  border-image: url("~@/./assets/img/border_image.png") 30 30 stretch;
  background: #18202d;
}
.part-four-responsive {
  width: 100%;
  height: 310px;
  border: 5px solid transparent;
  border-image: url("~@/./assets/img/border_image.png") 30 30 stretch;
  background: #18202d;
}
</style>
```

## 工作经验
>PartFive.vue


```js
<template>
  <div :class="partFive">
    <h3 class="text-center text-top">工作经验</h3>
    <p>
      <a href="javascript:void(0)">古德网络科技有限公司</a>
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
```


## 个人技能

除了工作经验，我们还需要 show 一下我们的编程技能都有什么：

>PartSix.vue

```js
<template>
  <div :class="partSix">
    <h3 class="text-center">编程技能</h3>
    <p class="font-small"><span class="font-bold">前端：</span>HTML/HTML5、CSS/CSS3、JS/ES6、jQuery、Vue</p>
  </div>
</template>

<script>
export default {
  name: "partSix",
  data() {
    return {
      partSix: "part-six",
      curWidth: 0
    };
  },
  beforeMount() {
    this.curWidth = document.documentElement.clientWidth || document.body.clientWidth;
    if(this.curWidth < 1600) {
      this.partSix = "part-six-responsive"
    }
  }
};
</script>

<style scoped>
.part-six {
  width: 100%;
  height: 310px;
  border: 40px solid transparent;
  border-image: url("~@/./assets/img/border_image.png") 30 30 stretch;
  background: #18202d;
}
.part-six-responsive {
  width: 100%;
  border: 40px solid transparent;
  border-image: url("~@/./assets/img/border_image.png") 30 30 stretch;
  background: #18202d;
}
.text-center {
  text-align: center;
}
.font-small {
  font-size: .9em;
}
.font-bold {
  font-weight: bold;
  color: deepskyblue;
}
</style>
```

## 求职意向
+	最后，当然要表明我们的求职意向，好让 HR 小姐姐知道我们想要什么啦~

>PartSeven.vue

```js
<template>
  <div :class="partSeven">
    <h3 class="text-center">求职意向</h3>
    <p class="text-small"><span class="font-bold">期望职位：</span>前端工程师</p>

    <p class="text-small"><span class="font-bold">目标城市：</span>杭州</p>
    <p class="text-small"><span class="font-bold">期望薪资：</span>12K-15K</p>
    <p class="text-small"><span class="font-bold">入职时间：</span>一个月内</p>
  </div>
</template>

<script>
export default {
  name: "partSeven",
  data() {
    return {
      partSeven: "part-seven",
      curWidth: 0
    };
  },
  beforeMount() {
    this.curWidth = document.documentElement.clientWidth || document.body.clientWidth;
    if(this.curWidth < 1600) {
      this.partSeven = "part-sevev-responsive"
    }
  }
};
</script>

<style scoped>
.part-seven {
  width: 100%;
  height: 310px;
  border: 40px solid transparent;
  border-image: url("~@/./assets/img/border_image.png") 30 30 stretch;
  background: #18202d;
}
.part-sevev-responsive {
  width: 100%;
  border: 40px solid transparent;
  border-image: url("~@/./assets/img/border_image.png") 30 30 stretch;
  background: #18202d;
}
.text-center {
  text-align: center;
}
.text-small {
  font-size: .9em;
}
.font-bold {
  text-align: center;
  color: deepskyblue;
}
</style>
```

简历到此为止就完工了，路过的给点个赞给个 star 吧