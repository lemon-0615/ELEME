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
       * 时间戳是当前系统时间，格式"yyyyMMddHHmmss"。时间戳有效时间为24小时，如：20140416142030
       * SigParameter参数需要大写，如不能写成sig=abcdefg而应该写成sig=ABCDEFG
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
      * 表单前台验证, 如果不通过, 提示(减少请求，减小后台压力)
      * 发送ajax请求, 得到返回的结果
      * 根据结果的标识(code)来判断登陆请求是否成功
           1: 不成功, 显示提示
           0. 成功, 保存用户信息，保存在state中的userInfo对象里, 返回到上次路由
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
### 模拟(mock)数据/接口（模拟数据）
  1. Web 应用前后端(台)分离:
      + 后台向前台提供 API 接口, 只负责数据的提供和计算，而完全不处理展现
      + 前台通过 Http(Ajax)请求获取数据, 在浏览器端动态构建界面显示数据
  2. 设计 JSON 数据结构
   * 理解 JSON 数据结构
     +  结构: 名称, 数据类型
     +  value
     +  value 可以变, 但结构不能变
   * 编写模拟 JSON 数据: src/mock/data.json,在商家信息中，主要分为三大块：info,goods,ratings
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
###  ShopHeader组件
   1. 异步显示数据效果的编码流程
      * ajax
          ajax请求函数
          接口请求函数
      * vuex
          state
          mutation-types
          actions
          mutations
      * 组件
          dispatch(): 异步获取后台数据到vuex的state
          mapState(): 从vuex的state中读取对应的数据
          模板中显示
      * 多个li标签，通过for循环，类名存放数组中，按顺序存放然后调用显示
   2. 初始显示异常
      * 情况1: Cannot read property 'xxx' of undefined"
       + 原因: 状态里的初始值是对象，对象里的数据是从后台异步获取，初始值是空对象, 内部没有数据, 而模块中直接显示3层表达式
       + 解决: 避免无数据时候进行了解析，使用v-if指令
        
      * 情况2: Cannot read property 'xxx' of null"
       + 原因：初始值为null，而模块中直接显示两层表达式
       + 解决初始值为{}
   3. vue transition动画
### ShopGoods组件
   1. 动态展现列表数据
   2. 基本滑动:
        * 使用better-scroll
        * 理解其基本原理
         * 什么时候形成滑动：有一个包裹的div，div的高度是固定的，被指定一个可视区域的固定高度，div里有一个列表ul，一旦ul的高度超过了div的高度就会形成滚动
        *  创建BScroll对象的时机
          * watch + $nextTick()
          * callback + $nextTick
        * better-scroll 对外暴露了一个 BScroll 的类，我们初始化只需要 new 一个类的实例即可。第一个参数就是我们 wrapper 的 DOM 对象，第二个是一些配置参数
          ```
            let wrapper = document.querySelector('.wrapper') 
            let scroll = new BScroll(wrapper, {})
          ```
       * better-scroll 的初始化时机很重要，因为它在初始化的时候，会计算父元素和子元素的高度和宽度，来决定是否可以纵向和横向滚动。故在初始化它的时候，必须确保父元素和子元素的内容已经正确渲染了
    3. 滑动右侧列表, 左侧同步更新
        * better-scroll禁用了原生的dom事件, 使用的是自定义事件
        * 绑定监听: scroll/scrollEnd
        * 滚动监听的类型: probeType
        * 列表滑动的3种类型： 1).手指触摸，2)惯性，3)编码
         * 分析:
          * 类名: current 标识当前分类
          * 设计一个计算属性: currentIndex（找出相关数据，然后想计算的逻辑
          * 根据哪些数据计算? 1).scrollY: 右侧滑动的Y轴坐标 (滑动过程时实时变化) , 2).tops: 所有右侧分类li的top组成的数组  (列表第一次显示后就不再变化)
         * 编码:
          * 在滑动过程中, 实时收集scrollY
          * 列表第一次显示后, 收集tops
          * 实现currentIndex的计算逻辑
    4. 点击左侧列表项, 右侧滑动到对应位置
        ```
          mounted () {
              this.$store.dispatch('getShopGoods', () => { // 数据更新后执行
                this.$nextTick(() => { // 列表数据更新显示后执行
                  this._initScroll()
                  this._initTops()
                })
              })
            },
           methods: {
              // 初试化滚动条
              _initScroll () {
                // 列表显示之后创建
                /* eslint-disable no-new */
                new BScroll('.menu-wrapper', {
                  click: true
                })
                this.foodsScroll = new BScroll('.foods-wrapper', {
                  probeType: 2, // 因为惯性滑动不会触发
                  click: true
                })
                // 给右侧列表绑定scroll监听
                this.foodsScroll.on('scroll', ({x, y}) => {
                  console.log(x, y)
                  this.scrollY = Math.abs(y)
                })
                // 给右侧列表绑定scroll结束的监听
                this.foodsScroll.on('scrollEnd', ({x, y}) => {
                  console.log('scrollEnd', x, y)
                  this.scrollY = Math.abs(y)
                })
              },
              // 初试化tops
              _initTops () {
                // 1. 初始化tops
                const tops = []
                let top = 0
                tops.push(top)
                // 2. 收集
                // 找到所有分类的li
                const lis = this.$refs.foodsUl.getElementsByClassName('food-list-hook')
                Array.prototype.slice.call(lis).forEach(li => {
                  top += li.clientHeight
                  tops.push(top)
                })
                // 3. 更新数据
                this.tops = tops
                console.log(tops)
              },
              clickMenuItem (index) {
                // console.log(index)
                // 使右侧列表滑动到对应的位置
                // 得到目标位置的scrollY
                const scrollY = this.tops[index]
                // 立即更新scrollY(让点击的分类项成为当前分类)
                this.scrollY = scrollY
                // 平滑滑动右侧列表
                this.foodsScroll.scrollTo(0, -scrollY, 300)
              },
              // 显示点击的food
              showFood (food) {
                // 设置food
                this.food = food
                // 显示food组件 (在父组件中调用子组件对象的方法)
                this.$refs.food.toggleShow()
              }
            },
          ```
 * Vue.js 提供了我们一个获取 DOM 对象的接口—— vm.$refs。在这里，我们通过了 this.$refs.*** 访问到了这个 DOM 对象，
 * 在 mounted 这个钩子函数里，this.$nextTick 的回调函数中初始化 better-scroll
 * 数据绑定：更新了数据，对应的界面发生改变
    
### CartControl组件
   1. 问题: 更新状态数据, 对应的界面不变化
      * 原因: 一般方法给一个已有绑定的对象中添加一个新的属性, 这个属性没有数据绑定
      * 解决:  Vue.set(obj, 'xxx', value)才有数据绑定
              this.$set(obj, 'xxx', value)才有数据绑定
### ShopCart组件
   1. 使用vuex管理购物项数据: cartFoods
   2. 解决几个功能性bug(购物车打开条件：isshow为true，
      * 如果购物车的总数量为0, 直接不显示，用计算属性listshow
      * 数量为0后购物车关闭了，但是ishow还是true，导致下一次加food的时候购物车又马上弹出来：totalCount为0的时候，让this.isShow = false
      * 点击了一下下栏的购物车之后也导致了ishow为true：只有当总数量大于0时切换，this.totalCount>0的时候，this.isShow = !this.isShow
          ```
             <div class="shopcart-list" v-show="listShow">
             <div class="list-mask" v-show="listShow" @click="toggleShow"></div>
             listShow: {
            // 如果总数量为0, 直接不显示
            get () {
              if (this.totalCount === 0) {
                return false
              }
              return this.isShow
            },
            set () {
              if (!this.totalCount) {
                this.isShow = false
              }
              if (!this.isShow) {
                this.$nextTick(() => {
                // 实现BScroll的实例是一个单例
                  if (!this.scroll) {
                    this.scroll = new BScroll('.list-content', {
                      click: true
                    })
                  } else {
                    this.scroll.refresh() // 让滚动条刷新一下: 重新统计内容的高度
                  }
                })
              }
            }
           }
          //方法 
          toggleShow () {
              // 只有当总数量大于0时切换
              if(this.totalCount>0) {
                this.isShow = !this.isShow
              }
            },
         ```
   4. 界面的展现是根据数据展现的
   5. 购物车列表的滑动
   6. 清空购物车
        ```
          在mutations.js中
           // 清除food中的count
          state.cartFoods.forEach(food => { food.count = 0 })
          // 移除购物车中所有购物项
         state.cartFoods = []
       ```
### Food组件
   1. 父子组件:
        子组件调用父组件的方法: 通过props将方法传递给子组件
        父组件调用子组件的方法: 通过ref找到子组件标签对象
   2. 事件冒泡，阻止事件冒泡事件，在点击监听里加stop，即@click.stop
### ShopRatings组件
   1. 列表的过滤显示
   2. 自定义过滤器
      *  用数值selectType的0，1，2的值分别代表不满意，满意，全部评价
      *  布尔值onlyShowText表示是否只显示有文本的
      *  得到相关数据，产生一个过滤新数组
      *  条件1：selectType: 0/1/2 or rateType: 0/1 即 selectType===2 || selectType===rateType
      *  条件2： onlyShowText: true/false or text: 有值/没值 即 !onlyShowText || text.length>0
      *  最后返回  return (selectType === 2 || selectType === rateType) && (!onlyShowText || text.length > 0)
        ```
           filterRatings () {
              // 得到相关数据
              const {ratings, onlyShowText, selectType} = this
              // 产生一个过滤新数组
              return ratings.filter(rating => {
                const {rateType, text} = rating
                 return (selectType === 2 || selectType === rateType) && (!onlyShowText || text.length > 0)
                })
             }
        ```
### ShopInfo组件
   1. 使用better-scroll实现两个方向的滑动：
          ```
            new BScroll('.shop-info')
            new BScroll('.pic-wrapper', {
              scrollX: true // 水平滑动
             })
          ```
   2. 通过JS动态操作样式
        ```
          // 动态计算ul的宽度
           const ul = this.$refs.picsUl
           const liWidth = 120
           const space = 6
           const count = this.info.pics.length
           ul.style.width = (liWidth + space) * count - space + 'px'
         ```
   3. 解决当前路由刷新异常的bug
     * 数据是异步获取的，会导致一开始this.info.pics为null
     * 在mount中直接if判断，如果数据还没有, 直接return结束
     * 为确保数据在更新后也可以滑动，用watch监视数据info
         ```
            watch: {
              info () { // 刷新流程--> 更新数据
                this.$nextTick(() => {
                  this._initScroll()
               })
             }
            }
         ```
### Search组件
   1. 根据关键字来异步搜索显示匹配的商家列表(形成带列表的多个路由路径
   2. 实现没有搜索结果的提示显示(用一个标视变量来实现，布尔值的noSearchShops，初始值为false，有searchShops的值的时候，值为true(在watch里进行变化))
###  项目优化
   1. 缓存路由组件对象，复用路由组件对象, 复用路由组件获取的后台数据
         ```
           在shop.vue组件里
           <keep-alive>
             <router-view />
           </keep-alive>
         ```
   2. 路由组件懒加载
      * 使用replace模式实现路由跳转 <router-link to="/shop/goods" replace>点餐</router-link>
      * 路由组件的函数，只有执行函数的时候才会加载路由组件
      
            ```
            const MSite = () => import('../pages/MSite/MSite.vue')
            const Search = () => import('../pages/Search/Search.vue')
            const Order = () => import('../pages/Order/Order.vue')
            const Profile = () => import('../pages/Profile/Profile.vue')
            ```
   3. 图片懒加载: vue-lazyload使用
      * 下载包npm install --save vue-loader
      * 在main.js里引入
          ```
          import VueLazyload from 'vue-lazyload'
          import loading from './common/img/loading.gif'
          Vue.use(VueLazyload, {
          loading
          })
          <img v-lazy="food.image">
          ```
   4. 分析打包文件并优化     
      * vue 脚手架提供了一个用于可视化分析打包文件的包 webpack-bundle-analyzer 和配置
      * 启用打包可视化: npm run build --report
      * 使用 date-fns 代替 moment
           ```
            // import moment from 'moment'
            // import {format} from 'date-fns'
            import format from 'date-fns/format'
            import Vue from 'vue'
            Vue.filter('dateString', function (value, formatStr) {
            // return moment(value).format(format || 'YYYY-MM-DD HH:mm:ss')
            return format(value, formatStr || 'YYYY-MM-DD HH:mm:ss')
            })
           ```
