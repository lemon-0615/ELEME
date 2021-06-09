# gshop-client

> A Vue.js project

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report

# run unit tests
npm run unit

# run e2e tests
npm run e2e

# run all tests
npm test
```

For a detailed explanation on how things work, check out the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).

## Part1
### 1. 项目开发准备
* 项目描述：描述项目是一个怎么样的项目，是做什么的，是一个前端分离的项目Web App，项目采用功能模块，模块化，组件化（vue是基于组件开发），工程化(脚手架)的模式开发。项目构建用webpack，eslint对项目进行检查，功能模块包含商家, 商品, 购物车，用户管理等多个模块；
* 技术选型：技术架构-后台应用技术架构为: Node + Express + Mongodb + Mongoose；前台应用技术架构为: vue + vuex + vue-router + webpack + ES6。前台的数据展现，数据交互-ajax请求，接口测试，模拟数据，
* API接口：一个接口是四个信息的集合，请求:1.请求地址，2.请求方式，3.请求参数的格式，响应：4.响应数据格式
* 你能从此项目中学到什么? 1.学习开发的方式；2.涉及一些插件和库的学习；

### 2. 开启项目开发
 + 使用脚手架创建项目
 + 安装所有依赖/指定依赖
 + 开发环境运行（在内存里打包，通过浏览器访问）
 + 生产环境打包与发布

### 3. 搭建项目整体界面结构
+ stylus的理解和使用
        结构化（嵌套的层次结构）, 变量, 函数/minxin(混合)
+ vue-router的理解和使用
        router-view/router-link/keep-alive
        $router: 路由器对象, 包含一些操作路由的功能函数, 来实现编程式导航(跳转路由)
        $route: 当前路由对象, 一些当前路由信息数据的容器, path/meta/query/params（所有组件都可以用）
+ 项目路由拆分
+ 底部导航组件: FooterGuide
+ 导航路由组件: Msite/Search/Order/Profile

### 4. 抽取组件
- 头部组件: HeaderTop, 通过slot来实现组件通信标签结构
- 商家列表组件: ShopList
    
### 5. 登陆路由组件
- 静态组件
- FooterGuide的显示/隐藏: 通过路由的meta
     
### 6. 后台项目
- 启动后台项目: 理解前后台分离
- 测试后台接口: 使用postman
- 修正接口文档

### 7. 前后台交互
- ajax请求库: axios
- ajax请求函数封装: axios + promise
- 接口请求函数封装: 每个后台接口
## 过程笔记
### FooterGuide
* 底部图标的亮起，在标签中加入on来决定
* 使用对象语法，类名加布尔值判断，利用请求路由路径等于当前路径时on生效:class="{on: '/msite'===$route.path}"
* 添加鼠标点击事件监听，@click="goTo('/msite')"实现点击图标即可点亮
```
<template>
    <div class="footer_guide">
    <span  class="guide_item" :class="{on: '/msite'===$route.path}" @click="goTo('/msite')">
      <span class="item_icon">
        <i class="iconfont icon-waimai"></i>
      </span>
      <span>外卖</span>
    </span>
    <a href="javascript:;" class="guide_item" :class="{on: '/search'===$route.path}" @click="goTo('/search')">
      <span class="item_icon">
        <i class="iconfont icon-search"></i>
      </span>
      <span>搜索</span>
    </a>
    <a href="javascript:;" class="guide_item" :class="{on: '/order'===$route.path}" @click="goTo('/order')">
      <span class="item_icon">
        <i class="iconfont icon-dingdan"></i>
      </span>
      <span>订单</span>
    </a>
    <a href="javascript:;" class="guide_item" :class="{on: '/profile'===$route.path}" @click="goTo('/profile')">
      <span class="item_icon">
        <i class="iconfont icon-geren"></i>
      </span>
      <span>我的</span>
    </a>
  </div>
</template>
<script>
export default {
  methods: {
    goTo (path) {
      this.$router.replace(path)
    }
  }
}
</script>
```
### HeaderTop头部标题子组件
* 完成HeaderTop.vue文件内容
* 在另外的父组件中引入该子组件
* 在相应的父组件中映射成标签
* 动态组件初试化显示
* 除了标题正文本外的文字，其余部分可以利用插槽slot，
```
父组件
 <!--首页头部-->
        <HeaderTop title="昌平区北七家宏福科技园(337省道北)">
          <span class="header_search" slot="left">
            <i class="iconfont icon-sousuo"></i>
          </span>
            <span class="header_login" slot="right">
            <span class="header_login_text">登录|注册</span>
          </span>
        </HeaderTop>
 <script>
import HeaderTop from '../../components/HeaderTop/HeaderTop.vue'
export default {
  components: {
    HeaderTop
  }
}
</script>

子组件
<template>
  <header class="header">
    <slot name="left"></slot>
    <span class="header_title">
      <span class="header_title_text ellipsis">{{title}}</span>
    </span>
    <slot name="right"></slot>
  </header>
</template>

<script>
export default {
  props: {
    title: String
  }
}
</script>
```
### ShopList商家信息子组件
```
<template>
   <div class="shop_container">
            <ul class="shop_list">
              <li class="shop_li border-1px">
                <a>
                  <div class="shop_left">
                    <img class="shop_img" src="./images/shop/1.jpg">
                  </div>
                  <div class="shop_right">
                    <section class="shop_detail_header">
                      <h4 class="shop_title ellipsis">锄禾日当午，汗滴禾下土</h4>
                      <ul class="shop_detail_ul">
                        <li class="supports">保</li>
                        <li class="supports">准</li>
                        <li class="supports">票</li>
                      </ul>
                    </section>
                    <section class="shop_rating_order">
                      <section class="shop_rating_order_left">
                        <div class="star star-24">
                          <span class="star-item on"></span>
                          <span class="star-item on"></span>
                          <span class="star-item on"></span>
                          <span class="star-item half"></span>
                          <span class="star-item off"></span>
                        </div>
                        <div class="rating_section">
                          3.6
                        </div>
                        <div class="order_section">
                          月售106单
                        </div>
                      </section>
                      <section class="shop_rating_order_right">
                        <span class="delivery_style delivery_right">饿了么专送</span>
                      </section>
                    </section>
                    <section class="shop_distance">
                      <p class="shop_delivery_msg">
                        <span>¥20起送</span>
                        <span class="segmentation">/</span>
                        <span>配送费约¥5</span>
                      </p>
                    </section>
                  </div>
                </a>
              </li>
              <li class="shop_li border-1px">
                <a>
                  <div class="shop_left">
                    <img class="shop_img" src="./images/shop/2.jpg">
                  </div>
                  <div class="shop_right">
                    <section class="shop_detail_header">
                      <h4 class="shop_title ellipsis">锄禾日当午，汗滴禾下土</h4>
                      <ul class="shop_detail_ul">
                        <li class="supports">保</li>
                        <li class="supports">准</li>
                        <li class="supports">票</li>
                      </ul>
                    </section>
                    <section class="shop_rating_order">
                      <section class="shop_rating_order_left">
                        <div class="star star-24">
                          <span class="star-item on"></span>
                          <span class="star-item on"></span>
                          <span class="star-item on"></span>
                          <span class="star-item on"></span>
                          <span class="star-item off"></span>
                        </div>
                        <div class="rating_section">
                          4.1
                        </div>
                        <div class="order_section">
                          月售106单
                        </div>
                      </section>
                      <section class="shop_rating_order_right">
                        <span class="delivery_style delivery_right">饿了么专送</span>
                      </section>
                    </section>
                    <section class="shop_distance">
                      <p class="shop_delivery_msg">
                        <span>¥20起送</span>
                        <span class="segmentation">/</span>
                        <span>配送费约¥5</span>
                      </p>
                    </section>
                  </div>
                </a>
              </li>
              <li class="shop_li border-1px">
                <a>
                  <div class="shop_left">
                    <img class="shop_img" src="./images/shop/3.jpg">
                  </div>
                  <div class="shop_right">
                    <section class="shop_detail_header">
                      <h4 class="shop_title ellipsis">锄禾日当午，汗滴禾下土</h4>
                      <ul class="shop_detail_ul">
                        <li class="supports">保</li>
                        <li class="supports">准</li>
                        <li class="supports">票</li>
                      </ul>
                    </section>
                    <section class="shop_rating_order">
                      <section class="shop_rating_order_left">
                        <div class="star star-24">
                          <span class="star-item on"></span>
                          <span class="star-item on"></span>
                          <span class="star-item on"></span>
                          <span class="star-item off"></span>
                          <span class="star-item off"></span>
                        </div>
                        <div class="rating_section">
                          3.2
                        </div>
                        <div class="order_section">
                          月售106单
                        </div>
                      </section>
                      <section class="shop_rating_order_right">
                        <span class="delivery_style delivery_right">饿了么专送</span>
                      </section>
                    </section>
                    <section class="shop_distance">
                      <p class="shop_delivery_msg">
                        <span>¥20起送</span>
                        <span class="segmentation">/</span>
                        <span>配送费约¥5</span>
                      </p>
                    </section>
                  </div>
                </a>
              </li>
              <li class="shop_li border-1px">
                <a>
                  <div class="shop_left">
                    <img class="shop_img" src="./images/shop/4.jpg">
                  </div>
                  <div class="shop_right">
                    <section class="shop_detail_header">
                      <h4 class="shop_title ellipsis">锄禾日当午，汗滴禾下土</h4>
                      <ul class="shop_detail_ul">
                        <li class="supports">保</li>
                        <li class="supports">准</li>
                        <li class="supports">票</li>
                      </ul>
                    </section>
                    <section class="shop_rating_order">
                      <section class="shop_rating_order_left">
                        <div class="star star-24">
                          <span class="star-item on"></span>
                          <span class="star-item on"></span>
                          <span class="star-item on"></span>
                          <span class="star-item half"></span>
                          <span class="star-item off"></span>
                        </div>
                        <div class="rating_section">
                          3.6
                        </div>
                        <div class="order_section">
                          月售106单
                        </div>
                      </section>
                      <section class="shop_rating_order_right">
                        <span class="delivery_style delivery_right">饿了么专送</span>
                      </section>
                    </section>
                    <section class="shop_distance">
                      <p class="shop_delivery_msg">
                        <span>¥20起送</span>
                        <span class="segmentation">/</span>
                        <span>配送费约¥5</span>
                      </p>
                    </section>
                  </div>
                </a>
              </li>
            </ul>
    </div>
</template>
```
### 是否展示底部导航FooterGuide
 * 在App.vue组件FooterGuide渲染标签处加入条件渲染，即<FooterGuide v-show="$route.meta.showFooter"/>
 * $route为当前路由
 * 需要展现FooterGuide的组件路由加属性meta，配置对象，加一个标识属性showFooter
```
  {
      path: '/msite',
      component: MSite,
      meta: {
        showFooter: true
      }
    },
  ```
### 封装ajax请求函数
* ajax请求函数模块，返回值: promise对象(异步返回的数据是: response.data)，向外默认暴露一个函数ajax (url, data={}, type='GET') 
```
import axios from 'axios'
export default function ajax (url, data={}, type='GET') {

  return new Promise(function (resolve, reject) {
    // 执行异步ajax请求
    let promise
    if (type === 'GET') {
      // 准备url query参数数据
      let dataStr = '' //数据拼接字符串
      Object.keys(data).forEach(key => {
        dataStr += key + '=' + data[key] + '&'
      })
      if (dataStr !== '') {
        dataStr = dataStr.substring(0, dataStr.lastIndexOf('&'))
        url = url + '?' + dataStr
      }
      // 发送get请求
      promise = axios.get(url)
    } else {
      // 发送post请求
      promise = axios.post(url, data)
    }
    promise.then(function (response) {
      // 成功了调用resolve()
      resolve(response.data)
    }).catch(function (error) {
      //失败了调用reject()
      reject(error)
    })
  })
}
```
* 包含n个接口请求函数的模块，函数的返回值: promise对象
```
import ajax from './ajax'
// const BASE_URL = 'http://localhost:4000'
const BASE_URL = '/api'

// 1、根据经纬度获取位置详情
export const reqAddress = (geohash) => ajax(`${BASE_URL}/position/${geohash}`)
// 2、获取食品分类列表
export const reqFoodCategorys = () => ajax(BASE_URL+'/index_category')
// 3、根据经纬度获取商铺列表
export const reqShops = (longitude, latitude) => ajax(BASE_URL+'/shops', {longitude, latitude})
// 4、根据经纬度和关键字搜索商铺列表
export const reqSearchShop = (geohash, keyword) => ajax(BASE_URL+'/search_shops', {geohash, keyword})
// 6、用户名密码登陆
export const reqPwdLogin = ({name, pwd, captcha}) => ajax(BASE_URL+'/login_pwd', {name, pwd, captcha}, 'POST')
// 7、发送短信验证码
export const reqSendCode = (phone) => ajax(BASE_URL+'/sendcode', {phone})
// 8、手机号验证码登陆
export const reqSmsLogin = (phone, code) => ajax(BASE_URL+'/login_sms', {phone, code}, 'POST')
// 9、根据会话获取用户信息
export const reqUserInfo = () => ajax(BASE_URL+'/userinfo')
// 10、用户登出
export const reqLogout = () => ajax(BASE_URL+'/logout')

/**
 * 获取商家信息
 */
export const reqShopInfo = () => ajax('/info')

/**
 * 获取商家评价数组
 */
export const reqShopRatings = () => ajax('/ratings')

/**
 * 获取商家商品数组
 */
export const reqShopGoods = () => ajax('/goods')
```

### 异步处理
1. 封装ajax: 
   * promise+axios封装ajax请求的函数
   * 封装每个接口对应的请求函数(能根据接口定义ajax请求函数)
   * 解决ajax的跨越域问题: 配置代理, 对代理的理解,对于浏览器而言，不知道代理的存在，浏览器提交的是对当前前台的请求，前台和后台都是运行在各自的服务器上，前台应用服务器还运行着一个代理的代码，前台应用发请求的时候是对前台端口的请求，代理程序拦截请求，向后台端口发送请求，进行转发请求。代理是是一些程序，运行在前台上，监听前台端口
 ```
 proxyTable: {
      '/api': { // 匹配所有以 '/api'开头的请求路径
        target: 'http://localhost:4000', // 代理目标的基础路径
        changeOrigin: true, // 支持跨域
        pathRewrite: {// 重写路径: 去掉路径中开头的'/api'
          '^/api': ''
        }
      }
      },
  ```
2.异步显示
  * 用vuex管理从后台获取的状态数据
  * 下载vuex
  * 首页需要管理的数据：当前地址，食物分类轮播列表，商家列表
  * vuex编码
     * 创建所有相关的模块: store/index|state|mutations|actions|getters|mutation-types 
     * vuex最核心的管理对象store
      ```
     import Vue from 'vue'
     import Vuex from 'vuex'
     import state from './state'
     import mutations from './mutations'
     import actions from './actions.js'
     import getters from './getters'
     Vue.use(Vuex)

     export default new Vuex.Store({
      state,
      mutations,
      actions,
      getters
      })
    ```
     * 设计state: 从后台获取的数据
  ```
 export default {
    latitude: 40.10038, // 纬度
    longitude: 116.36867, // 经度
    address: {}, //地址相关信息对象
    categorys: [], // 食品分类数组
    shops: [], // 商家数组
    userInfo: {}, // 用户信息
    goods: [], // 商品列表
    ratings: [], // 商家评价列表
    info: {}, // 商家信息
    cartFoods: [], // 购物车中食物的列表
    searchShops: [], // 搜索得到的商家列表
}
  ```
  
   * 实现actions: 
        * 定义异步action: async/await
        * 流程: 发ajax获取数据, commit给mutation     
      ```
        // 异步获取地址
        async getAddress ({commit, state}) {
        // 发送异步ajax请求
          const geohash = state.latitude + ',' + state.longitude
          const result = await reqAddress(geohash)
          // 提交一个mutation
          if (result.code === 0) {
            const address = result.data
            commit(RECEIVE_ADDRESS, {address})
          }
        }     
      ```
   * 实现mutations: 给状态赋值  
     ```
     [RECEIVE_ADDRESS] (state, {address}) {
      state.address = address
     },
     ```
   * 实现index: 创建store对象
  ```
   /* vuex最核心的管理对象store */
      import Vue from 'vue'
      import Vuex from 'vuex'
      import state from './state'
      import mutations from './mutations'
      import actions from './actions.js'
      import getters from './getters'

      Vue.use(Vuex)

      export default new Vuex.Store({
        state,
        mutations,
        actions,
        getters
      })
   ```
  * main.js: 配置store   
3. 组件异步显示数据
   * import {mapState} from 'vuex'
   * 在mounted()通过$store.dispatch('actionName')来异步获取后台数据到state中
   * mapState(['xxx'])读取state中数据到组件中
   * 在模板中显示xxx的数据
4. 模板中显示数据的来源
   * data: 自身的数据(内部改变)
   * props: 外部传入的数据(外部改变)
   * computed: 根据data/props/别的compute/state/getters
5. 异步显示轮播图
   * 通过vuex获取foodCategorys数组(发请求, 读取)
   * 对数据进行整合计算(一维变为特定的二维数组)
   * 使用Swiper显示轮播, 如何在界面更新之后创建Swiper对象?
   
        1). 使用回调+$nextTick()   
        2). 使用watch+$nextTick()	 进行监视，一旦有数据，进行触发回调
    * vm.$nextTick([callback]) 用法：将回调延迟到下次DOM更新循环之后执行。在修改数据之后立即使用它，然后等待DOM更新。它跟全局方法Vue.nextTick一样，不同的是回调的this自动绑定到调用它的实例上。
    * 注意：一维变为特定的二维数组， 根据categorys一维数组生成一个2维数组，小数组中的元素个数最大是8
   ```
    categorysArr () {
      const {categorys} = this
      // 准备空的2维数组
      const arr = []
      // 准备一个小数组(最大长度为8)
      let minArr = []
      // 遍历categorys
      categorys.forEach(c => {
      // 如果当前小数组已经满了, 创建一个新的
        if (minArr.length === 8) {
          minArr = []
        }
        // 如果minArr是空的, 将小数组保存到大数组中
        if (minArr.length === 0) {
          arr.push(minArr)
        }
        // 将当前分类保存到小数组中
        minArr.push(c)
      })
      return arr
    }
   ```
    * 注意：监视列表categorys函数， categorys数组中有了数据，在异步更新界面之前执行
  ```
  watch: {
    categorys (value) { // categorys数组中有了数据，在异步更新界面之前执行
    /* eslint-disable no-new */
    // 界面更新就立即创建Swiper对象
      this.$nextTick(() => { // 一旦完成界面更新, 立即调用(此条语句要写在数据更新之后)
      // 创建一个Swiper实例对象, 来实现轮播
        new Swiper('.swiper-container', {
          loop: true,
          pagination: {
            el: '.swiper-pagination'
          }
        })
      })
    }
  },
 ```
* 网页里需要显示大量的图片，加载很慢，很长时间才回来，先显示SVG图（像一个轮廓)
 ```
<ul class="shop_list" v-if="shops.length">

 <ul v-else>
      <li v-for="item in 6" :key="item.text">
         <img src="./images/shop_back.svg" alt="back">
      </li>
  ```
 * Star组件：在div便签内，显示类名，但是有变化'star-'+size，
 * Star组件：for循环内，starClasses数组根据计算产生，即计算属性
 ```
 <template>
  <div class="star" :class="'star-'+size"> <!--显示类名，但是有变化'star-'+size-->
    <span class="star-item" v-for="(sc, index) in starClasses" :class="sc" :key="index"></span> <!--starClasses数组根据计算产生，即计算属性-->
  </div>
</template>

<script>
// 类名常量
const CLASS_ON = 'on'
const CLASS_HALF = 'half'
const CLASS_OFF = 'off'
export default {
  props: {
    score: Number,
    size: Number
  },
  computed: {
    /*
      3.2: 3 + 0 + 2
      3.5: 3 + 1 + 1
       */
    starClasses () {
      // 准备好分数
      const {score} = this
      const scs = []
      // 向scs中添加n个CLASS_ON
      const scoreInteger = Math.floor(score)
      for (let i = 0; i < scoreInteger; i++) {
        scs.push(CLASS_ON)
      }
      // 向scs中添加0/1个CLASS_HALF
      if (score * 10 - scoreInteger * 10 >= 5) {
        scs.push(CLASS_HALF)
      }
      // 向scs中添加n个CLASS_OFF
      while (scs.length < 5) {
        scs.push(CLASS_OFF)
      }
      return scs
    }
  }
}
</script>
 ```
###  登陆/注册: 界面相关效果
1. 切换登陆方式
   * 用一个标识符loginWay来切换登陆方式
2. 手机号合法检查
   * 在获取验证码的按钮上绑定计算属性rightPhone，利用正则表达式判断
3. 倒计时效果
   * 异步获取短信验证码，设置一个函数getCode
   * 在验证码按钮的文本显示使用三目表达式
4. 切换显示或隐藏密码
   * 在密码的input标签用两个输入框转换显示，文本text和密码password的类型，用v-if，v-else使用布尔值shoPwd进行切换
   * 用div绘制切换按钮开关，用showPwd的值判断开关状态是on还是off
   * 开关switch_button off绑定点击事件监听进行切换状态，点一次就进行取反
   * 开关的圈圈的移动通过样式来实现 &.right transform translateX(30px)
5. 前台验证提示
### 前后台交互相关问题
   1. 如何查看你的应用是否发送某个ajax请求?  
      * 浏览器的network
   2. 发ajax请求404
      * 请求的路径的对
      * 代理是否生效(配置和重启)
      * 服务器应用是否运行
   3. 后台返回了数据, 但页面没有显示?
      * 检查vuex中是否有
      * 检查组件中是否读取
   4. 动态一次性短信验证码:用容联云通讯
     * 使用MD5加密（账户Id + 账户授权令牌 + 时间戳）。其中账户Id和账户授权令牌根据url的验证级别对应主账户。
        时间戳是当前系统时间，格式"yyyyMMddHHmmss"。时间戳有效时间为24小时，如：20140416142030
        SigParameter参数需要大写，如不能写成sig=abcdefg而应该写成sig=ABCDEFG
     * 用Base64编码（账户Id + 冒号 + 时间戳）其中账户Id根据url的验证级别对应主账户，冒号为英文冒号，时间戳是当前系统时间，格式"yyyyMMddHHmmss"，需与SigParameter中时间戳相同。
     * 发送请求, 并得到返回的结果, 调用callback
 ### 完成登陆/注册功能
   1. 2种方式
      * 手机号/短信验证码登陆
      * 用户名/密码/图片验证码登陆
      * 验证码图片绑定点击转换函数，函数中每次指定的src路径要不一样,通过增加日期值改变
       ```
      <img class="get_verification" src="http://localhost:4000/captcha" alt="captcha" @click="getCaptcha" ref="captcha">
       // 获取一个新的图片验证码
      getCaptcha () {
      // 每次指定的src路径要不一样,通过增加日期值改变
      this.$refs.captcha.src = 'http://localhost:4000/captcha?time=' + Date.now()
      }
      ```
   2. 登陆的基本流程
      * 表单前台验证, 如果不通过, 提示
      * 发送ajax请求, 得到返回的结果
      * 根据结果的标识(code)来判断登陆请求是否成功
           1: 不成功, 显示提示
           0. 成功, 保存用户信息, 返回到上次路由
      * 使用移动端组件库mint-ui
   3. vue自定义事件
      * 绑定监听: @eventName="fn"  function fn (data) {// 处理}
      * 分发事件: this.$emit('eventName', data)
   4. 注意:
      * 使用network查看请求(路径/参数/请求方式/响应数据)
      * 使用vue的chrome插件查看vuex中的state和组件中的数据
      * 使用debugger语句调试代码
      * 实参类型与形参类型的匹配问题       
       
### 搭建商家整体界面
  1. 拆分界面路由
     + 商家头部ShopHead；商家商品ShopGoods；商家评价ShopRatings；商家信息ShopInfo
  2. 路由的定义/配置|使用
### 模拟(mock)数据/接口
  1. Web 应用前后端(台)分离:
      + 后台向前台提供 API 接口, 只负责数据的提供和计算，而完全不处理展现
      + 前台通过 Http(Ajax)请求获取数据, 在浏览器端动态构建界面显示数据
  2. 设计 JSON 数据结构
   1).理解 JSON 数据结构
   
   +  结构: 名称, 数据类型
   +  value
   +  value 可以变, 但结构不能变
  2).编写模拟 JSON 数据: src/mock/data.json,在商家信息中，主要分为三大块：info,goods,ratings
  3. 利用 mockjs 提供模拟数据
    + Mockjs: 用来拦截 ajax 请求, 生成随机数据返回
    + 使用mockjs提供mock数据接口
    ```
      import Mock from 'mockjs'
      import data from './data.json'

      // 返回goods的接口
      Mock.mock('/goods', {code: 0, data: data.goods})
      // 返回ratings的接口
      Mock.mock('/ratings', {code: 0, data: data.ratings})
      // 返回info的接口
      Mock.mock('/info', {code: 0, data: data.info})

      // export default ???  不需要向外暴露任何数据, 只需要保存能执行即可
     ```
