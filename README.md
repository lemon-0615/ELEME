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

## 搭建项目整体界面结构
    stylus的理解和使用
        结构化, 变量, 函数/minxin(混合)
    vue-router的理解和使用
        router-view/router-link/keep-alive
        $router: 路由器对象, 包含一些操作路由的功能函数, 来实现编程式导航(跳转路由)
        $route: 当前路由对象, 一些当前路由信息数据的容器, path/meta/query/params
    项目路由拆分
    底部导航组件: FooterGuide
    导航路由组件: Msite/Search/Order/Profile
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
