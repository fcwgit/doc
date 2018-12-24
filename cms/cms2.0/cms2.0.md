# 1、评论功能

## 1.1、分析

> 1、文本框双向数据绑定。
>
> 2、为发表按钮绑定一个事件。
>
> 3、校验评论功能是否为空，如果为空则提示客户评论内容不可为空。
>
> 4、通过vue-resource发送请求，将评论内容发送给服务器。
>
> 5、当发表评论ok后，重新刷新列表，以查看最新的评论。（目的：查看最新评论。）
>
> +如果调用getComments方法重新刷新评论列表的话，可能只能得到最后一页的评论，前几页的评论获取不到
>
> +换一种思路：当评论成功后，在客户端，手动拼接一个最新的评论对象，然后调用数组的unshift方法，把最新的评论追加到data中comments的开头。完美实现刷新评论列表的功能。

![1545611399079](E:\IdeaProjects\doc\cms2.0\assets\1545611399079.png)

![1545611414223](E:\IdeaProjects\doc\cms2.0\assets\1545611414223.png)

![1545611482419](E:\IdeaProjects\doc\cms2.0\assets\1545611482419.png)

![1545611897075](E:\IdeaProjects\doc\cms2.0\assets\1545611897075.png)

> 使用json格式接收响应数据

![1545612056249](E:\IdeaProjects\doc\cms2.0\assets\1545612056249.png)

![1545612120023](E:\IdeaProjects\doc\cms2.0\assets\1545612120023.png)

![1545612547645](E:\IdeaProjects\doc\cms2.0\assets\1545612547645.png)

> 发送请求，并将数据添加到当前数组队列

![1545612602460](E:\IdeaProjects\doc\cms2.0\assets\1545612602460.png)

# 2、图片分享

## 2.1、配置首页路由

![1545615137572](E:\IdeaProjects\doc\cms2.0\assets\1545615137572.png)

![1545615445547](E:\IdeaProjects\doc\cms2.0\assets\1545615445547.png)

![1545615570047](E:\IdeaProjects\doc\cms2.0\assets\1545615570047.png)

![1545615586303](E:\IdeaProjects\doc\cms2.0\assets\1545615586303.png)

![1545615623651](E:\IdeaProjects\doc\cms2.0\assets\1545615623651.png)

![1545615635731](E:\IdeaProjects\doc\cms2.0\assets\1545615635731.png)

## 2.2、顶部导航条制作

>1、顶部的滑动条。
>
>2、底部的图片列表。

![1545615828316](E:\IdeaProjects\doc\cms2.0\assets\1545615828316.png)

> MUI中有对应的组件

![1545617119587](E:\IdeaProjects\doc\cms2.0\assets\1545617119587.png)

> 由于 .mui-fullscreen样式，导致全屏显示，删除 .mui-fullscreen 样式

![1545617199717](E:\IdeaProjects\doc\cms2.0\assets\1545617199717.png)

>正常显示滑动条了

### 2.2.1、坑

> 1、需要借助MUI的tab-top-webview-main.html。
>
> 2、需要把slider区域的mui-fullscreen样式去掉。
>
> 3、滑动条无法正常滑动，通过官方文档发现滑动条是js组件，需要初始化
>
> + 导入mui.js
>
> + ```javascript
>   mui('.mui-scroll-wrapper').scroll({
>   	deceleration: 0.0005 //flick 减速系数，系数越大，滚动速度越慢，滚动距离越小，默认值0.0006
>   });
>   ```
>
> + 调用官方提供的初始化方法
>
> 4、我们在初始化滑动条，导入了mui.js，但是控制台报错：Uncaught TypeError: 'caller', 'callee', and 'arguments' properties may not be accessed on strict mode
>
> + 经过合理推测，可能是mui.js使用了 'caller', 'callee', and 'arguments' ，但是webpack打包好的bundle.js中，默认是启用严格模式的，所以两者冲突了。
> + 方案1：在webpack中禁用严格模式。
> + 方案2：把mui.js中的非严格模式的代码改掉。
>
> 5、刚进入页面无法滑动、
>
> + 初始化时机很重要，在mounted生命周期函数初始化mui
> + 如果要初始化滑动条，必须等DOM加载完毕，所以把初始化滑动条的代码搬到mounted生命周期函数。
>
> 6、底部tabbar无法切换
>
> 需要把每个tabbar按钮的样式中'mui-tab-item'重新改一下名字

### 2.2.2、MUI——scroll初始化

![1545617438856](E:\IdeaProjects\doc\cms2.0\assets\1545617438856.png)

![1545617478080](E:\IdeaProjects\doc\cms2.0\assets\1545617478080.png)

### 2.2.3、MUI——js

![1545617528644](E:\IdeaProjects\doc\cms2.0\assets\1545617528644.png)



![1545617834004](E:\IdeaProjects\doc\cms2.0\assets\1545617834004.png)

![1545617818628](E:\IdeaProjects\doc\cms2.0\assets\1545617818628.png)

> 报错：严格模式不允许使用caller、callee、grguments
>
> import mui from "../../lib/js/mui.min.js";导致的上述问题

### 2.2.4、移除严格模式

> babel-plugin-transform-remove-strict-mode https://www.npmjs.com/package/babel-plugin-transform-remove-strict-mode

![1545618420546](E:\IdeaProjects\doc\cms2.0\assets\1545618420546.png)

![1545618526616](E:\IdeaProjects\doc\cms2.0\assets\1545618526616.png)

![1545619995913](E:\IdeaProjects\doc\cms2.0\assets\1545619995913.png)

![1545620052070](E:\IdeaProjects\doc\cms2.0\assets\1545620052070.png)

![1545620108483](E:\IdeaProjects\doc\cms2.0\assets\1545620108483.png)

> 可以滑动了

### 2.2.5、测试

>Unable to preventDefault inside passive event listener due to target being treated as passive.

![1545620745261](E:\IdeaProjects\doc\cms2.0\assets\1545620745261.png)

touch-action属性的含义：https://zhidao.baidu.com/question/1928098737368855187.html

![1545620855426](E:\IdeaProjects\doc\cms2.0\assets\1545620855426.png)

> 问题：
>
> 1、初始进入滑动条页面，是不可以滑动的，需要刷新页面才可以滑动。
>
> 2、底部tabbar出错，无法切换

### 2.2.6、scroll初始化时机

![1545621157859](E:\IdeaProjects\doc\cms2.0\assets\1545621157859.png)

> 当组件中的DOM结构被渲染好并放到页面中后，会执行这个钩子函数
>
> 只有当.mui-scroll-wrapper渲染到DOM后，mui函数才能获取这个节点，并挂载初始化
>
> 如果要操作元素，最好在mounted函数中进行处理

### 2.2.7、tabbar无法点击问题

> 同样由于引入mui的js导致的

![1545629307736](E:\IdeaProjects\doc\cms2.0\assets\1545629307736.png)

> 具体因为mu的js与mui-tab-item样式冲突
>
> 修改mui-tab-item

![1545629440843](E:\IdeaProjects\doc\cms2.0\assets\1545629440843.png)

![1545629855666](E:\IdeaProjects\doc\cms2.0\assets\1545629855666.png)



![1545629720172](E:\IdeaProjects\doc\cms2.0\assets\1545629720172.png)

## 2.3、分类数据

### 2.3.1、获取数据

![1545630494468](E:\IdeaProjects\doc\cms2.0\assets\1545630494468.png)

![1545630729147](E:\IdeaProjects\doc\cms2.0\assets\1545630729147.png)



![1545630737399](E:\IdeaProjects\doc\cms2.0\assets\1545630737399.png)

### 2.3.2、设置选中样式

![1545630900130](E:\IdeaProjects\doc\cms2.0\assets\1545630900130.png)

> 将class设置为计算模式

![1545630916913](E:\IdeaProjects\doc\cms2.0\assets\1545630916913.png)



## 2.4、图片列表数据

### 2.4.1、懒加载控件mint-ui——Lazyload

`引入`

```javascript
import { Lazyload } from 'mint-ui';

Vue.use(Lazyload);
```

`例子`

> 为 `img` 元素添加 `v-lazy` 指令，指令的值为图片的地址。同时需要设置图片在加载时的样式。

```html
<ul>
  <li v-for="item in list">
    <img v-lazy="item">
  </li>
</ul>

img[lazy=loading] {
  width: 40px;
  height: 300px;
  margin: auto;
}
```

> 若列表不在 window 上滚动，则需要将被滚动元素的 id 属性以修饰符的形式传递给 `v-lazy` 指令

```html
<div id="container">
  <ul>
    <li v-for="item in list">
      <img v-lazy.container="item">
    </li>
  </ul>
</div>
```

![1545632150295](E:\IdeaProjects\doc\cms2.0\assets\1545632150295.png)

![1545632167786](E:\IdeaProjects\doc\cms2.0\assets\1545632167786.png)

![1545632184150](E:\IdeaProjects\doc\cms2.0\assets\1545632184150.png)

![1545632197619](E:\IdeaProjects\doc\cms2.0\assets\1545632197619.png)

![1545632264336](E:\IdeaProjects\doc\cms2.0\assets\1545632264336.png)

![1545633032913](E:\IdeaProjects\doc\cms2.0\assets\1545633032913.png)

![1545632911626](E:\IdeaProjects\doc\cms2.0\assets\1545632911626.png)

### 2.4.2、懒加载样式

> 全量引入mint-ui

![1545633431457](E:\IdeaProjects\doc\cms2.0\assets\1545633431457.png)

### 2.4.3、调整图片列表样式

![1545633854837](E:\IdeaProjects\doc\cms2.0\assets\1545633854837.png)

![1545633867890](E:\IdeaProjects\doc\cms2.0\assets\1545633867890.png)

### 2.4.4、添加文字描述

![1545633982809](E:\IdeaProjects\doc\cms2.0\assets\1545633982809.png)

![1545633992391](E:\IdeaProjects\doc\cms2.0\assets\1545633992391.png)

![1545634572338](E:\IdeaProjects\doc\cms2.0\assets\1545634572338.png)

![1545634588268](E:\IdeaProjects\doc\cms2.0\assets\1545634588268.png)

![1545634631879](E:\IdeaProjects\doc\cms2.0\assets\1545634631879.png)

![1545634670890](E:\IdeaProjects\doc\cms2.0\assets\1545634670890.png)

![1545634740335](E:\IdeaProjects\doc\cms2.0\assets\1545634740335.png)

![1545634751917](E:\IdeaProjects\doc\cms2.0\assets\1545634751917.png)

## 2.5、图片详情

![1545636820280](E:\IdeaProjects\doc\cms2.0\assets\1545636820280.png)

> 改造为router-link

![1545636885003](E:\IdeaProjects\doc\cms2.0\assets\1545636885003.png)

![1545636954212](E:\IdeaProjects\doc\cms2.0\assets\1545636954212.png)

![1545637039158](E:\IdeaProjects\doc\cms2.0\assets\1545637039158.png)

![1545637051335](E:\IdeaProjects\doc\cms2.0\assets\1545637051335.png)

![1545637121352](E:\IdeaProjects\doc\cms2.0\assets\1545637121352.png)



![1545637239060](E:\IdeaProjects\doc\cms2.0\assets\1545637239060.png)

> 点击图片跳转到详情界面

![1545637229107](E:\IdeaProjects\doc\cms2.0\assets\1545637229107.png)

### 2.5.1、详情界面

![1545640949236](E:\IdeaProjects\doc\cms2.0\assets\1545640949236.png)

![1545640970516](E:\IdeaProjects\doc\cms2.0\assets\1545640970516.png)

![1545641015600](E:\IdeaProjects\doc\cms2.0\assets\1545641015600.png)



```javascript
<template>
  <div class="photoinfo-container">
    <h3>{{photoInfo.title}}</h3>
    <p class="subtitle">
      <span>发表时间:{{photoInfo.add_time | dateFormat}}</span>
      <span>点击:{{photoInfo.click}}次</span>
    </p>
    <hr>
    <!-- 缩略图区域 -->
    <!-- 图片内容区 -->
    <div class="content" v-html="photoInfo.content"></div>

    <!-- 评论子组件（放置一个现成的） -->
    <cmt-box :id="id"></cmt-box>
  </div>
</template>
<script>
// 1、导入评论子组件
import comment from "../subcomponents/comment.vue";

export default {
  data() {
    return {
      id: this.$route.params.id, //从路由中获取到的图片id
      photoInfo: {
        add_time: "2018-12-21T14:25:22+08:00",
        click: 10,
        title: "色香味俱全的美味佳肴",
        id: 1,
        content:
          "色香味俱全的美味佳肴6色香味俱全的美味佳肴6色香味俱全的美味佳肴6色香味俱全的美味佳肴6色香味俱全的美味佳肴6色香味俱全的美味佳肴"
      } //图片详情
    };
  },
  components: {
    "cmt-box": comment
  },
  created() {
    //   this.getPhotoInfo();
  },
  methods: {
    getPhotoInfo() {
      // 获取图片的详情
      this.$http
        .get("api/getPhotoInfo/" + this.id)
        .then(result => {
          if (result.body.status === 0) {
            this.photoInfo = result.body.message;
          }
        })
        .catch(err => {});
    }
  }
};
</script>

<style lang="scss" scoped>
.photoinfo-container {
  padding: 3px;
  h3 {
    color: #26a2ff;
    font-size: 15px;
    text-align: center;
    margin: 15px 0;
  }
  .subtitle {
    display: flex;
    justify-content: space-between;
    font-size: 13px;
  }
  .content {
    font-size: 13px;
    line-height: 30px;
  }
}
</style>

```

![1545640912249](E:\IdeaProjects\doc\cms2.0\assets\1545640912249.png)

### 2.5.2、vue-preview plugin缩略图

https://github.com/LS1231/vue-preview

![1545641144920](E:\IdeaProjects\doc\cms2.0\assets\1545641144920.png)

![1545641300746](E:\IdeaProjects\doc\cms2.0\assets\1545641300746.png)

![1545641440398](E:\IdeaProjects\doc\cms2.0\assets\1545641440398.png)

![1545641555826](E:\IdeaProjects\doc\cms2.0\assets\1545641555826.png)

![1545641796589](E:\IdeaProjects\doc\cms2.0\assets\1545641796589.png)

![1545641810415](E:\IdeaProjects\doc\cms2.0\assets\1545641810415.png)

![1545641824911](E:\IdeaProjects\doc\cms2.0\assets\1545641824911.png)

![1545642022725](E:\IdeaProjects\doc\cms2.0\assets\1545642022725.png)

![1545642029780](E:\IdeaProjects\doc\cms2.0\assets\1545642029780.png)



# 3、商品

## 3.1、分析

> 1、修改首页路由
>
> 2、商品列表页面
>
> 3、配置路由

![1545643366897](E:\IdeaProjects\doc\cms2.0\assets\1545643366897.png)

![1545643534631](E:\IdeaProjects\doc\cms2.0\assets\1545643534631.png)

![1545643480696](E:\IdeaProjects\doc\cms2.0\assets\1545643480696.png)

![1545643543432](E:\IdeaProjects\doc\cms2.0\assets\1545643543432.png)

















































