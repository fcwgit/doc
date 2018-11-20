## 1、复习：

## 1.1、无法安装依赖

有时候使用`npm i node-sass -D`装不上，这时候，就必须使用 `cnpm i node-sass -D`

## 1.2、npm init -y包管理文件

> 注意：如果创建的项目的根目录名称包含中文，此时不可使用-y命令
>
> npm init回车后，需要输入项目名称（当根目录包含中文的时候需要使用此命令，不可加-y参数）

![1542542668848](assets/1542542668848.png)

## 1.3、创建其他目录及文件

> src：源码
>
> dist：打包后生成的文件
>
> index.html：项目首页
>
> main.js：项目的js入口文件

![1542542750002](assets/1542542750002.png)

## 1.4、打包webpack  src  des

![1542542820210](assets/1542542820210.png)

**注意：如果不创建dist目录，webpack命令也会自动创建此目录**

![1542542881699](assets/1542542881699.png)

## 1.5、打包测试

![1542542927999](assets/1542542927999.png)

![1542542943064](assets/1542542943064.png)

**后台输出了  ok**

## 1.6、自动打包webpack-dev-server

帮助系统实时打包

### 1.6.1、安装依赖包

> npm i webpack-dev-server -D

![1542543301623](assets/1542543301623.png)

### 1.6.2、创建webpack.config.js配置文件

![1542543367529](assets/1542543367529.png)

### 1.6.3、安装webpack（当前目录安装）

![1542543405887](assets/1542543405887.png)

**提示依赖webpack**

![1542543469842](assets/1542543469842.png)

## 1.7、配置webpack

**由于webpack是基于Node进行构建的，所以，webpack的配置文件中，任何合法的Node代码都是支持的**

![1542543580258](assets/1542543580258.png)

![1542543653343](assets/1542543653343.png)

**注意：此时并不没有实现自动构建**

![1542543778370](assets/1542543778370.png)

## 1.8、开启实时构建package.json

> 查看webpack安装情况

![1542543847672](assets/1542543847672.png)

> 配置实时更新、热更新、自动打开网页

![1542543977504](assets/1542543977504.png)

![1542544064909](assets/1542544064909.png)

> webpack托管的目录为  /  根目录下没有对应的bundle.js
>
> ![1542637355762](assets/1542637355762.png)

## 1.9、html-webpack-plugin

**将网页加载到内存，并自动引用打包后的js文件**

### 1.9.1、安装插件

![1542544143240](assets/1542544143240.png)

### 1.9.2、引入插件(webpack.config.js)

![1542544229843](assets/1542544229843.png)

![1542544306721](assets/1542544306721.png)

## 1.10、测试

![1542544337791](assets/1542544337791.png)

![1542544360022](assets/1542544360022.png)

## 1.11、引入css

### 1.11.1、创建css相关目录

![1542544455128](assets/1542544455128.png)

### 1.11.2、创建index.css文件

![1542544496118](assets/1542544496118.png)

### 1.11.3、引用css

**在index.html中直接引用css，将导致多发送一次http请求**

**将css文件通过webpack进行打包，在main.js文件中引入css文件**

![1542544625298](assets/1542544625298.png)

![1542544684183](assets/1542544684183.png)

## 1.12、引入第三方loader（style-loader、css-loader）

![1542544763907](assets/1542544763907.png)

## 1.13、配置第三方loader

![1542544826207](assets/1542544826207.png)

## 1.14、支持less

![1542544946246](assets/1542544946246.png)

![1542544982871](assets/1542544982871.png)

## 1.15、支持sass

![1542545072881](assets/1542545072881.png)

![1542545031627](assets/1542545031627.png)

![1542545104832](assets/1542545104832.png)

![1542545156789](assets/1542545156789.png)

![1542545254063](assets/1542545254063.png)

![1542545179890](assets/1542545179890.png)

## 

# 2、webpack中url-loader的使用

## 2.1、创建图片目录

![1542545395285](assets/1542545395285.png)

## 2.2、配置sass

![1542545452822](assets/1542545452822.png)

## 2.3、测试

![1542545527348](assets/1542545527348.png)

## 2.4、分析，引入第三方插件

![1542545581639](assets/1542545581639.png)

![1542545619679](assets/1542545619679.png)

![1542545671995](assets/1542545671995.png)

![1542545720639](assets/1542545720639.png)

> url-loader依赖file-loader，无需单独配置file-loader

## 2.5、测试

![1542545712614](assets/1542545712614.png)

![1542545791204](assets/1542545791204.png)

![1542545844240](assets/1542545844240.png)

**减少图片的二次请求**

## 2.6、url-loader优化

**只对小图片进行base64处理，大图片不建议进行base64处理**

### 2.6.1、limit参数

![1542546016452](assets/1542546016452.png)

![1542546053743](assets/1542546053743.png)

![1542546094645](assets/1542546094645.png)

![1542546124312](assets/1542546124312.png)

![1542546208793](assets/1542546208793.png)

### 2.6.2、name、ext参数

![1542546264436](assets/1542546264436.png)

>name：name=[name]表示图片原名
>
>ext：name=[name].[ext]表示图片原名、扩展名保持不变

![1542546298070](assets/1542546298070.png)

![1542546359009](assets/1542546359009.png)

![1542546374310](assets/1542546374310.png)

## 2.7、重名文件的问题

![1542546540837](assets/1542546540837.png)

![1542546573696](assets/1542546573696.png)

**不对文件重新命名**

![1542546588918](assets/1542546588918.png)

![1542546652567](assets/1542546652567.png)

![1542546704929](assets/1542546704929.png)

![1542546779232](assets/1542546779232.png)

![1542546846082](assets/1542546846082.png)

![1542546862822](assets/1542546862822.png)

## 2.8、引用字体图标

### 2.8.1、引入bootstrap样式库

![1542547225602](assets/1542547225602.png)

![1542546959508](assets/1542546959508.png)

### 2.8.2、引用红心图标

![1542547018169](assets/1542547018169.png)

### 2.8.3、原始方法引入bootstrap

![1542547161229](assets/1542547161229.png)

![1542547262450](assets/1542547262450.png)

### 2.8.4、在main.js中引入bootstrap

![1542547419665](assets/1542547419665.png)

![1542547445358](assets/1542547445358.png)

![1542547473968](assets/1542547473968.png)

### 2.8.5、配置字体处理loader

![1542547509137](assets/1542547509137.png)

### 2.8.6、测试

![1542547578688](assets/1542547578688.png)

![1542547594556](assets/1542547594556.png)



# 3、总结webpack

## 3.1、json中不可以写注释

![1542550443956](assets/1542550443956.png)

## 3.2、本地运行找不到包

> 全局安装了webpack是不够的，还需要在本地安装

![1542550640942](assets/1542550640942.png)

**解决方法：npm i 重新安装相关包**

![1542550732752](assets/1542550732752.png)

![1542550792457](assets/1542550792457.png)

# 4、babel高级语法转换

## 4.1、class关键字

![1542550884946](assets/1542550884946.png)

**之前定义对象的方式：**

![1542550943967](assets/1542550943967.png)

### 4.1.1、静态属性

![1542551026761](assets/1542551026761.png)

![1542551083817](assets/1542551083817.png)

> 传统方式定义的静态属性

![1542639745778](assets/1542639745778.png)

![1542551140150](assets/1542551140150.png)

### 4.1.2、静态属性和实例属性挂载的地方完全不一样

![1542639909401](assets/1542639909401.png)

![1542639997599](assets/1542639997599.png)

### 4.1.3、无法解析class语法

![1542551957872](assets/1542551957872.png)



**运行报错，无法处理es6高级语法**

![1542640057576](assets/1542640057576.png)



## 4.2、安装以及配置babel

### 4.2.1、原理

![1542551368053](assets/1542551368053.png)

![1542551461737](assets/1542551461737.png)

![1542551529511](assets/1542551529511.png)



![1542551660794](assets/1542551660794.png)

### 4.2.2、安装包

![1542640372553](assets/1542640372553.png)

![1542640406410](assets/1542640406410.png)

### 4.2.3、配置babel来转换高级的ES语法

![1542551708259](assets/1542551708259.png)



## 4.3、.babelrc高级语法解析配置文件

![1542551794128](assets/1542551794128.png)

![1542551807351](assets/1542551807351.png)

![1542551833842](assets/1542551833842.png)

![1542551900179](assets/1542551900179.png)

![1542551914585](assets/1542551914585.png)

## 4.4、说明

![1542552122247](assets/1542552122247.png)

**第一套为转换器**

**第二套为语法对应关系**

![1542552260441](assets/1542552260441.png)



# 5、render

## 5.1、在普通页面中渲染组件

![1542552358327](assets/1542552358327.png)

> 将login组件放到div下面，不会删掉div	

## 5.2、render

![1542552464300](assets/1542552464300.png)



![1542552536140](assets/1542552536140.png)

![1542552580682](assets/1542552580682.png)

![1542640915902](assets/1542640915902.png)

## 5.3、优缺点

![1542552685653](assets/1542552685653.png)

![1542552698551](assets/1542552698551.png)

**传统component组件方式：类似于传值表达式，可以放很多的组件**

![1542552709807](assets/1542552709807.png)

![1542552718500](assets/1542552718500.png)



**render：方式是直接替换，一个vm中只能有一个render组件**



# 6、webpack项目中使用vue

## 6.1、复习，普通网页如何使用vue

![1542553290937](assets/1542553290937.png)

## 6.2、webpack使用vue

![1542553384805](assets/1542553384805.png)

![1542553439887](assets/1542553439887.png)

![1542553420807](assets/1542553420807.png)

**无法正常运行**

![1542553508968](assets/1542553508968.png)

![1542553551623](assets/1542553551623.png)

## 6.3、分析

![1542553804539](assets/1542553804539.png)

![1542553732275](assets/1542553732275.png)

![1542553707857](assets/1542553707857.png)

![1542553778620](assets/1542553778620.png)

**只是导入了：dist/vue.runtime.common.js**

![1542553846858](assets/1542553846858.png)

![1542553886058](assets/1542553886058.png)

## 6.4、解决方案

### 6.4.1、方案一

![1542553953301](assets/1542553953301.png)

![1542553964605](assets/1542553964605.png)

### 6.4.2、方案二

![1542554134687](assets/1542554134687.png)

![1542554169529](assets/1542554169529.png)

![1542554197755](assets/1542554197755.png)

也可以正常运行了



# 7、在runtime-only的时候如何渲染组件

## 7.1、vue纯粹的组件，由三部分组成

![1542642110332](assets/1542642110332.png)

![1542642151057](assets/1542642151057.png)

## 7.2、将login.vue渲染到index.html

![1542642185803](assets/1542642185803.png)

### 7.2.1、导入login组件

![1542642271115](assets/1542642271115.png)

![1542642289969](assets/1542642289969.png)

> webpack解析不了使用vue定义的模板
>
> 需要引入第三方包，将vue解析为js，然后交由webpack进行打包

### 7.2.2、安装第三方插件

![1542642455892](assets/1542642455892.png)

![1542642470602](assets/1542642470602.png)

### 7.2.3、配置第三方插件

![1542642531576](assets/1542642531576.png)

![1542642569759](assets/1542642569759.png)

### 7.2.4、使用render渲染vue组件

![1542642640472](assets/1542642640472.png)

![1542642665687](assets/1542642665687.png)

![1542642694379](assets/1542642694379.png)

![1542642711359](assets/1542642711359.png)

![1542642816896](assets/1542642816896.png)

## 7.2、在webpack中配置.vue组件页面的总结

![1542642975668](assets/1542642975668.png)

1. 运行`cnpm i vue -S`将vue安装为运行依赖；

2. 运行`cnpm i vue-loader vue-template-compiler -D`将解析转换vue的包安装为开发依赖；

3. 运行`cnpm i style-loader css-loader -D`将解析转换CSS的包安装为开发依赖，因为.vue文件中会写CSS样式；

4. 在`webpack.config.js`中，添加如下`module`规则：

```
module: {
    rules: [
      { test: /\.css$/, use: ['style-loader', 'css-loader'] },
      { test: /\.vue$/, use: 'vue-loader' }
    ]
  }
```

5. 创建`App.js`组件页面：

```
    <template>
      <!-- 注意：在 .vue 的组件中，template 中必须有且只有唯一的根元素进行包裹，一般都用 div 当作唯一的根元素 -->
      <div>
        <h1>这是APP组件 - {{msg}}</h1>
        <h3>我是h3</h3>
      </div>
    </template>
    <script>
    // 注意：在 .vue 的组件中，通过 script 标签来定义组件的行为，需要使用 ES6 中提供的 export default 方式，导出一个vue实例对象
    export default {
      data() {
        return {
          msg: 'OK'
        }
      }
    }
    </script>
    <style scoped>
    h1 {
      color: red;
    }
    </style>
```

6. 创建`main.js`入口文件：

```
    // 导入 Vue 组件
    import Vue from 'vue'
    // 导入 App组件
    import App from './components/App.vue'
    // 创建一个 Vue 实例，使用 render 函数，渲染指定的组件
    var vm = new Vue({
      el: '#app',
      render: c => c(App)
    });
```

## 7.3、在使用webpack构建的Vue项目中使用模板对象？

1. 在`webpack.config.js`中添加`resolve`属性：
```
resolve: {
    alias: {
      'vue$': 'vue/dist/vue.esm.js'
    }
  }
```



# 8、export default和export

> ES6中语法使用总结

1. 使用 `export default` 和 `export` 导出模块中的成员; 对应ES5中的 `module.exports` 和 `export`

2. 使用 `import ** from **` 和 `import '路径'` 还有 `import {a, b} from '模块标识'` 导入其他模块

3. 使用箭头函数：`(a, b)=> { return a-b; }`



## 8.1、vue组件中的data必须是function，且返回对象

![1542643129850](assets/1542643129850.png)

![1542722852173](assets/1542722852173.png)



## 8.2、export  default 和export的使用方式

![1542723039912](assets/1542723039912.png)

![1542723080136](assets/1542723080136.png)

![1542723129038](assets/1542723129038.png)

> 注意：要么使用es6的导入、导出，要么使用node的导入、导出，配套使用，不可混用 

## 8.3、使用es6向外暴露一个对象

![1542723237580](assets/1542723237580.png)

## 8.4、在main.js使用import导入上面的对象

![1542723287071](assets/1542723287071.png)

![1542723345235](assets/1542723345235.png)



## 8.5、注意

![1542723438890](assets/1542723438890.png)

![1542723520910](assets/1542723520910.png)

![1542723490885](assets/1542723490885.png)



## 8.6、export var  

![1542723594529](assets/1542723594529.png)

![1542723889808](assets/1542723889808.png)

![1542723643716](assets/1542723643716.png)

## 8.7、注意export var按需导出

![1542723987793](assets/1542723987793.png)

![1542723952401](assets/1542723952401.png)

![1542723972272](assets/1542723972272.png)

> 1、按需导出
>
> 2、接收名称不可变
>
> 3、若想重命名，则可以使用as起别名

![1542724127749](assets/1542724127749.png)

![1542724163743](assets/1542724163743.png)





# 9、在vue组件页面中，集成vue-router路由模块

[vue-router官网](https://router.vuejs.org/)

1. 安装依赖

   ```
   npm i vue-router
   ```

2. 导入路由模块：

```

import VueRouter from 'vue-router'

```

2. 安装路由模块：

```

Vue.use(VueRouter);

```

3. 导入需要展示的组件:

```

import login from './components/account/login.vue'

import register from './components/account/register.vue'

```

4. 创建路由对象:

```

var router = new VueRouter({

  routes: [

    { path: '/', redirect: '/login' },

    { path: '/login', component: login },

    { path: '/register', component: register }

  ]

});

```

5. 将路由对象，挂载到 Vue 实例上:

```

var vm = new Vue({

  el: '#app',

  // render: c => { return c(App) }

  render(c) {

    return c(App);

  },

  router // 将路由对象，挂载到 Vue 实例上

});

```

6. 改造App.vue组件，在 template 中，添加`router-link`和`router-view`：

```

    <router-link to="/login">登录</router-link>

    <router-link to="/register">注册</router-link>



    <router-view></router-view>

```

## 9.1、初始化项目



 ![1542724402806](assets/1542724402806.png)

## 9.2、安装vue-router

![1542724454388](assets/1542724454388.png)

![1542724525999](assets/1542724525999.png)

## 9.3、创建两个组件

![1542724592879](assets/1542724592879.png)

## 9.4、导入组件、创建路由对象

![1542724771622](assets/1542724771622.png)

## 9.5、将路由对象挂载到vm上

![1542724809167](assets/1542724809167.png)

## 9.6、将路由挂载到index.html

![1542724879300](assets/1542724879300.png)

![1542724919246](assets/1542724919246.png)

> 由于render会替换被挂载组件上面的所有标签

![1542725015761](assets/1542725015761.png)

![1542725120726](assets/1542725120726.png)

![1542725142071](assets/1542725142071.png)

![1542725699732](assets/1542725699732.png)

# 10、子路由

## 10.1、创建子组件

![1542725827455](assets/1542725827455.png)



## 10.2、推荐vscode插件

![1542725865184](assets/1542725865184.png)

## 10.3、创建子组件内容

![1542725904281](assets/1542725904281.png)

## 10.4、注册子组件

![1542726011940](assets/1542726011940.png)

![1542726044475](assets/1542726044475.png)

![1542726067455](assets/1542726067455.png)





# 11、组件中的css作用域问题

![1542726131817](assets/1542726131817.png)

![1542726200702](assets/1542726200702.png)	

## 11.1、全局样式

![1542726242880](assets/1542726242880.png)



## 11.2、局部样式

![1542726282237](assets/1542726282237.png)

![1542726269828](assets/1542726269828.png)

##  11.3、scss或less

![1542726332807](assets/1542726332807.png)

![1542726384763](assets/1542726384763.png)

> 设置斜体

![1542726456499](assets/1542726456499.png)

## 11.4、建议

![1542726520237](assets/1542726520237.png)



# 12、抽离路由为单独的模块

## 12.1、创建router.js

![1542726583828](assets/1542726583828.png)



## 12.2、将路由信息配置在router.js

> 注意router.js与引入组件的目录层级关系

![1542726708631](assets/1542726708631.png)

## 12.3、把路由对象暴露出去

![1542726902562](assets/1542726902562.png)

## 12.4、导入路由配置信息

![1542726841423](assets/1542726841423.png)

## 使用 饿了么的 MintUI 组件

[Github 仓储地址](https://github.com/ElemeFE/mint-ui)

[Mint-UI官方文档](http://mint-ui.github.io/#!/zh-cn)

1. 导入所有MintUI组件：

```

import MintUI from 'mint-ui'

```

2. 导入样式表：

```

import 'mint-ui/lib/style.css'

```

3. 在 vue 中使用 MintUI：

```

Vue.use(MintUI)

```

4. 使用的例子：

```

<mt-button type="primary" size="large">primary</mt-button>

```



## 使用 MUI 组件

[官网首页](http://dev.dcloud.net.cn/mui/)

[文档地址](http://dev.dcloud.net.cn/mui/ui/)

1. 导入 MUI 的样式表：

```

import '../lib/mui/css/mui.min.css'

```

2. 在`webpack.config.js`中添加新的loader规则：

```

{ test: /\.(png|jpg|gif|ttf)$/, use: 'url-loader' }

```

3. 根据官方提供的文档和example，尝试使用相关的组件



## 将项目源码托管到oschina中

1. 点击头像 -> 修改资料 -> SSH公钥 [如何生成SSH公钥](http://git.mydoc.io/?t=154712)

2. 创建自己的空仓储，使用 `git config --global user.name "用户名"` 和 `git config --global user.email ***@**.com` 来全局配置提交时用户的名称和邮箱

3. 使用 `git init` 在本地初始化项目

4. 使用 `touch README.md` 和 `touch .gitignore` 来创建项目的说明文件和忽略文件；

5. 使用 `git add .` 将所有文件托管到 git 中

6. 使用 `git commit -m "init project"` 将项目进行本地提交

7. 使用 `git remote add origin 仓储地址`将本地项目和远程仓储连接，并使用origin最为远程仓储的别名

8. 使用 `git push -u origin master` 将本地代码push到仓储中



## App.vue 组件的基本设置

1. 头部的固定导航栏使用 `Mint-UI` 的 `Header` 组件；

2. 底部的页签使用 `mui` 的 `tabbar`;

3. 购物车的图标，使用 `icons-extra` 中的 `mui-icon-extra mui-icon-extra-cart`，同时，应该把其依赖的字体图标文件 `mui-icons-extra.ttf`，复制到 `fonts` 目录下！

4. 将底部的页签，改造成 `router-link` 来实现单页面的切换；

5. Tab Bar 路由激活时候设置高亮的两种方式：

 + 全局设置样式如下：

 ```

 	.router-link-active{

      	color:#007aff !important;

    }

 ```

 + 或者在 `new VueRouter` 的时候，通过 `linkActiveClass` 来指定高亮的类：

 ```

 	// 创建路由对象

    var router = new VueRouter({

      routes: [

        { path: '/', redirect: '/home' }

      ],

      linkActiveClass: 'mui-active'

    });

 ```



## 实现 tabbar 页签不同组件页面的切换

1. 将 tabbar 改造成 `router-link` 形式，并指定每个连接的 `to` 属性；

2. 在入口文件中导入需要展示的组件，并创建路由对象：

```

    // 导入需要展示的组件

    import Home from './components/home/home.vue'

    import Member from './components/member/member.vue'

    import Shopcar from './components/shopcar/shopcar.vue'

    import Search from './components/search/search.vue'



    // 创建路由对象

    var router = new VueRouter({

      routes: [

        { path: '/', redirect: '/home' },

        { path: '/home', component: Home },

        { path: '/member', component: Member },

        { path: '/shopcar', component: Shopcar },

        { path: '/search', component: Search }

      ],

      linkActiveClass: 'mui-active'

    });

```



## 使用 mt-swipe 轮播图组件

1. 假数据：

```

lunbo: [

        'http://www.itcast.cn/images/slidead/BEIJING/2017440109442800.jpg',

        'http://www.itcast.cn/images/slidead/BEIJING/2017511009514700.jpg',

        'http://www.itcast.cn/images/slidead/BEIJING/2017421414422600.jpg'

      ]

```

2. 引入轮播图组件：

```

<!-- Mint-UI 轮播图组件 -->

    <div class="home-swipe">

      <mt-swipe :auto="4000">

        <mt-swipe-item v-for="(item, i) in lunbo" :key="i">

          <img :src="item" alt="">

        </mt-swipe-item>

      </mt-swipe>

    </div>

  </div>

```



## 在`.vue`组件中使用`vue-resource`获取数据

1. 运行`cnpm i vue-resource -S`安装模块

2. 导入 vue-resource 组件

```

import VueResource from 'vue-resource'

```

3. 在vue中使用 vue-resource 组件

```

Vue.use(VueResource);

```