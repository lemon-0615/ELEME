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
   * 解决ajax的跨越域问题: 配置代理, 对代理的理解
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
        2). 使用watch+$nextTick()	
