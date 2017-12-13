# 微信小程序的相关操作

* [页面跳转](#页面跳转)
* [banner的显示](#banner的显示)
* [多个图片横向排列](#多个图片横向排列)
* [列表显示](#列表显示)
* [下拉列表](#下拉列表)
* [查询框](#查询框)
* [评星控件](#评星控件)

## 页面跳转
三种页面跳转的方法  
1. wx.navigateTo(OBJECT)

    保留当前页面，跳转到应用内的某个页面，使用wx.navigateBack可以返回到原页面。  
    OBJECT参数说明： 
    
    参数/类型/必填/说明  
    url/String/是/需要跳转的应用内页面的路径，路径后可以带参数。参数与路径之间使用?分隔，参数键与参数值用=相连，不同参数用&分隔；如‘path?key=value&key2=value2’  
    success/Function/否/接口调用成功的回调函数  
    fail/Function/否/接口调用失败的回调函数  
    complete/Function/否/接口调用结束的回调函数（调用成功、失败都会执行）

2. wx.redirectTo(OBJECT)  

    关闭当前页面，跳转到应用内的某个页面。  
    OBJECT参数说明：
    
    参数/类型/必填/说明  
    url/String/是/需要跳转的应用内页面的路径 
    success/Function/否/接口调用成功的回调函数 
    fail/Function/否/接口调用失败的回调函数 
    complete/Function/否/接口调用结束的回调函数（调用成功、失败都会执行）

3. wx.navigateBack(OBJECT)  

    关闭当前页面，返回上一页面或多级页面。可通过 getCurrentPages()) 获取当前的页面栈，决定需要返回几层。  
    OBJECT参数说明：
    
    参数/类型/默认值/说明 
    delta/Number/1/返回的页面数，如果delta大于现有页面数，则返回到首页。

## banner的显示
wxml中
```
  <swiper class='banners' indicator-dots="true" autoplay="true" interval="4000" duration="1000" indicator-color="#60ffffff" indicator-active-color="#fff">
    <block wx:for="{{banner}}" wx:key="*this">
      <swiper-item>
        <image src="{{item}}" class="banner" mode="aspectFill"></image>
      </swiper-item>
    </block>
  </swiper>
```
js中
```
    banner: ['http://i.dxlfile.com/adm/material/2016_12_12/20161212135600242250.jpg',
      'http://i.dxlfile.com/adm/material/2017_01_04/2017010411165785666.jpg',
      'http://i.dxlfile.com/adm/material/2017_01_04/20170104140739205869.jpg',
      'http://i.dxlfile.com/adm/material/2017_01_16/20170116171332214897.jpg']
```
wxss中
```
.banner{
    width: 100%;
    height: 411rpx;
}
```

## 多个图片横向排列
多个图片菜单类选项
wxml中
```
  <view class='funcs'>
    <view class='func' wx:for="{{functions}}" wx:for-item='item' wx:key='item.id' data-id="{{item.id}}">
      <image src="{{item.url}}" mode="aspectFill"></image>
      <view class='name'>{{item.name}}</view>
    </view>
  </view>
```
js中
```
    functions: [
      {
        url: '../../images/i01.png',
        name: '婚礼策划',
        id: '01'
      },
      {
        url: '../../images/i02.png',
        name: '婚纱摄影',
        id: '02'
      },
      {
        url: '../../images/i03.png',
        name: '婚宴酒店',
        id: '03'
      },
      {
        url: '../../images/i04.png',
        name: '婚礼用车',
        id: '04'
      },
      {
        url: '../../images/i05.png',
        name: '婚礼用品',
        id: '05'
      },
      {
        url: '../../images/i06.png',
        name: '金银首饰',
        id: '06'
      },
    ]
```
wxss中
```
.funcs{
    background-color: #ffffff;
    width: 100%;
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    padding: 20rpx 0 0rpx 0;
}

.funcs .func{
    width: 25%;
    text-align: center;
    margin-bottom: 30rpx;
}
.funcs .func image{
    width: 100rpx;
    height: 100rpx;
  text-align: center;

}
.funcs .func .name{
    text-align: center;
    color: #666666;
    font-size: 26rpx;
    margin-top: 10rpx;
}
```

## 列表显示
wxml中
```
<import src="../../components/good/good.wxml"/>
  <view class='maylike'>
  <view class='title'>猜你喜欢</view>
  <view class='goods'>

  <block  wx:for="{{goods}}" wx:for-item='good' wx:key='*this' >

    <template is="good" data="{{good:good}}"/>
  </block>
  
  </view>
  </view>
```
js中
```
    goods: [
      {
        url: 'http://p1.meituan.net/wedding/5c683d257d0a418c146308b455bb5b582651471.jpg%40640w_480h_0e_1l%7Cwatermark%3D0',
        name: '热烈如初',
        price: '13800',
        oldprice: '19800',
        sell: '5',
        address: '二环路东五段万达广场8单元2101(近成仁公交站)',
        km: '1.1km'
      },
      {
        url: 'http://p1.meituan.net/wedding/adf460e1e88714cb30e118387de0b09e3536225.jpg%40640w_480h_0e_1l%7Cwatermark%3D0',
        name: '全包好超值无敌到爆宇宙套餐',
        price: '8800',
        oldprice: '10800',
        sell: '20',
        address: '东大街芷泉段88号时代豪庭(香格里拉酒店)',
        km: '1.8km'
      },
      {
        url: 'http://p0.meituan.net/wedding/4972ddf9c2067c193f6408f006f818c02213163.jpg%40640w_480h_0e_1l%7Cwatermark%3D0',
        name: '林中奇缘',
        price: '15800',
        oldprice: '20800',
        sell: '15',
        address: '总府路46号1-4楼(盐市口红旗商场斜对面)',
        km: '2.4km'
      },
      {
        url: 'http://p1.meituan.net/wedding/8a40a46c24c3f812586853aa5d5cb56d3134895.jpg%40640w_480h_0e_1l%7Cwatermark%3D0',
        name: '清新云系婚礼经典款',
        price: '12900',
        oldprice: '15800',
        sell: '25',
        address: '天府新区益州大道588号益州国际写字楼10楼',
        km: '3.4km'
      },
      {
        url: 'http://p1.meituan.net/wedding/5c683d257d0a418c146308b455bb5b582651471.jpg%40640w_480h_0e_1l%7Cwatermark%3D0',
        name: '热烈如初',
        price: '13800',
        oldprice: '19800',
        sell: '5',
        address: '二环路东五段万达广场8单元2101(近成仁公交站)',
        km: '1.1km'
      },
      {
        url: 'http://p1.meituan.net/wedding/adf460e1e88714cb30e118387de0b09e3536225.jpg%40640w_480h_0e_1l%7Cwatermark%3D0',
        name: '全包好超值无敌到爆宇宙套餐',
        price: '8800',
        oldprice: '10800',
        sell: '20',
        address: '东大街芷泉段88号时代豪庭(香格里拉酒店)',
        km: '1.8km'
      },
      {
        url: 'http://p0.meituan.net/wedding/4972ddf9c2067c193f6408f006f818c02213163.jpg%40640w_480h_0e_1l%7Cwatermark%3D0',
        name: '林中奇缘',
        price: '15800',
        oldprice: '20800',
        sell: '15',
        address: '总府路46号1-4楼(盐市口红旗商场斜对面)',
        km: '2.4km'
      },
      {
        url: 'http://p1.meituan.net/wedding/8a40a46c24c3f812586853aa5d5cb56d3134895.jpg%40640w_480h_0e_1l%7Cwatermark%3D0',
        name: '清新云系婚礼经典款',
        price: '12900',
        oldprice: '15800',
        sell: '25',
        address: '天府新区益州大道588号益州国际写字楼10楼',
        km: '3.4km'
      }
    ]
```
wxss中
```
@import '../../components/good/good.wxss';
.maylike{
    background-color: #fff;
    margin-top: 30rpx;
padding-top: 20rpx;
}

.maylike .title{
    color: #808080;
    font-size: 28rpx;
margin-left: 28rpx;
margin-bottom: -10rpx;

}
```
注：在wxss中需要添加引用template的wxss样式  
good.wxml中
```
<template name='good'>
	<view class='good' >
		<image src="{{good.url}}" mode="aspectFill"></image>
		<view class='mask'></view>
		<view class='info'>
			<view class='title'>
				<text>{{good.name}}</text>
			</view>
			<view class='detail'>
				<view class='timeinfo'>
				<text>{{good.address}}</text>
				
				</view>
				<view class='address' >
				<text>{{good.km}}</text>
				
				</view>
			</view>

		</view>

		<view class='bottom'>
		<view class='price'>￥{{good.price}}</view>
		<view class='oldprice'>￥{{good.oldprice}}</view>
		<view class='selled'>已售{{good.sell}}</view>
		</view>
	</view>
</template>
```
good.wxss中
```
.good {
  overflow: hidden;
  position: relative;
  border-radius: 8rpx;
  margin: 25rpx;
}

.good image {
  width: 100%;
  height: 375rpx;
  vertical-align: bottom;
}

.good .mask {
  position: absolute;
  top: 0;
  left: 0;
  z-index: 1;
  height: 100%;
  width: 560rpx;
  border-top-left-radius: 8rpx;
  border-bottom-left-radius: 8rpx;
  background: linear-gradient(to right, rgba(0, 0, 0, 0.6)0, rgba(0, 0, 0, 0)100%);
}

.good .info {
  position: absolute;
  top: 30rpx;
  left: 12rpx;
  z-index: 2;
  overflow: hidden;
}

.good .info .title {
  color: #fff;
  font-size: 40rpx;
  margin-bottom: 10rpx;
}

.info .title text {
  overflow: hidden;
  text-overflow: ellipsis;
  text-shadow: 2rpx 2rpx rgba(0, 0, 0, 0.4);
  -webkit-line-clamp: 2;
  display: -webkit-box;
  -webkit-box-orient: vertical;
}

.good .detail {
  position: relative;
  padding-left: 36rpx;
}

.good .detail .timeinfo {
  color: #fff;
  font-size: 22rpx;
  line-height: 1;
}

.good .timeinfo text {
  margin-right: 20rpx;
}

.good .address {
  color: #fff;
  font-size: 22rpx;
  line-height: 1;
  margin-top: 6rpx;
}

.good  .detail::before {
  content: '';
  position: absolute;
  top: 4rpx;
  left: 24rpx;
  width: 6rpx;
  height: 100%;
  background-color: #4abdcc;
}

.good .userinfo {
  position: absolute;
  left: 25rpx;
  bottom: 35rpx;
  z-index: 2;
}

.good .userinfo image {
  width: 50rpx;
  height: 50rpx;
  border-radius: 50rpx;
}

.good .userinfo .username {
  margin-left: 15rpx;
  color: #fff;
  font-size: 20rpx;
  vertical-align: middle;
}

.good .bottom {
  position: absolute;
  left: 25rpx;
  bottom: 20rpx;
  z-index: 2;
  color: #fff;
  font-size: 22rpx;
  display: flex;
  flex-wrap: nowrap;
  flex-direction: row;
  width: 660rpx;
  align-items: flex-end;
}

.bottom .price {
  color: #f63;
  font-size: 30rpx;
  margin-right: 14rpx;
}

.bottom .oldprice {
  color: #fff;
  font-size: 22rpx;
  text-decoration: line-through;
  flex: 1;
}

.bottom .selled {
  color: #ffffff;
  font-size: 22rpx;
}

```

## 下拉列表
wxml中
```
  <view class='navbtns'>
    <view class='navitem nearby' bindtap='navitation' data-id='01'>
      附近
      <image src="{{selectedNav === '01' ? '../../images/arrow_up.png' : '../../images/arrow_down.png'}}"></image>
    </view>
    <view class='line'></view>
    <view class='navitem sort' bindtap='navitation' data-id='02'>
      全部分类
      <image src="{{selectedNav === '02' ? '../../images/arrow_up.png' : '../../images/arrow_down.png'}}"></image>
    </view>
    <view class='line'></view>
    <view class='navitem rank' bindtap='navitation' data-id='03'>
      排序
      <image src="{{selectedNav === '03' ? '../../images/arrow_up.png' : '../../images/arrow_down.png'}}"></image>
    </view>
  </view>
  <view class='wrap'>
    <scroll-view class='scroller' scroll-y="true" lower-threshold="800">
    </scroll-view>
    <view class='spinner' wx:if='{{showspinner}}'>
      <view class='items'>
        <block wx:for="{{spinners}}" wx:for-item='item' wx:key="item.id">
          <view class='item' bindtap='spinnerclick'>{{item.name}}</view>
        </block>
      </view>
    </view>
  </view>
```
wxss中
```
.navbtns{
    display: flex;
    height: 80rpx;
    flex-wrap: nowrap;
    flex-direction: row;
    align-items: center;
    background-color: #ffffff;
}

.navbtns .navitem{
    flex: 1;
    text-align: center;
    color: #777777;
    font-size: 26rpx;
    height: 80rpx;
    line-height: 80rpx;
}
.navbtns .navitem image{
    display: inline-block;
    width: 26rpx;
    height: 26rpx;
    margin-left: 6rpx;
    vertical-align: middle;
}

.navbtns .line{
width: 3rpx;
background-color: #aaaaaa;
height: 45rpx;
flex-shrink: 0;
}

.wrap{
    position: relative;
}

.wrap .spinner{
    position: absolute;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, .6);
    z-index: 1;
    top: 0;
    left: 0;
}

.wrap .spinner .items{
    background-color: #fff;
    padding-left: 20rpx;
}

.wrap .spinner .items .item{
   padding-left: 25rpx;
border-bottom: 1rpx solid #777777;
height: 90rpx;
line-height: 90rpx;
color: #333;
font-size: 30rpx;

}


.scroller{
    margin-top: -5rpx;
}
```
js中
```
        selectedNav: '00',
        showspinner: false,
        nearby: [
            {
                name: '附近（智能范围）',
                id: 'a01',
            },
            {
                name: '500米',
                id: 'a02',
            },
            {
                name: '1000米',
                id: 'a03',
            },
            {
                name: '2000米',
                id: 'a04',
            },
            {
                name: '5000米',
                id: 'a05',
            },
        ],
        sort: [
            {
                name: '全部',
                id: 'b00'
            },
            {
                name: '婚礼策划',
                id: 'b01'
            },
            {
                name: '婚纱摄影',
                id: 'b02'
            },
            {
                name: '婚宴酒店',
                id: 'b03'
            },
            {
                name: '婚礼用车',
                id: 'b04'
            },
            {
                name: '婚礼用品',
                id: 'b05'
            },
            {
                name: '金银首饰',
                id: 'b06'
            },
        ],
        rank: [
            {
                name: '智能排序',
                id: 'c00',
            },
            {
                name: '离我最近',
                id: 'c01',
            },
            {
                name: '人气最高',
                id: 'c02',
            },
            {
                name: '评价最好',
                id: 'c03',
            },
            {
                name: '人均最低',
                id: 'c04',
            },
            {
                name: '人均最高',
                id: 'c05',
            },
        ],
        spinners: []
        
        
            navitation(event) {
                let id = event.currentTarget.dataset.id;
                const that = this;
                console.log(id);
                if (id == that.data.selectedNav) {
                    id = '00';
                    that.setData({
                        showspinner: false,
                    })
                } else {
                    that.setData({
                        showspinner: true,
                    })
                }
                console.log(id);
                that.setData({
                    selectedNav: id,
                })
                let temps = that.data.spinners;
                if (id == '02') {
                    temps = that.data.sort;
                } else if (id == '03') {
                    temps = that.data.rank;
                } else if (id == '01') {
                    temps = that.data.nearby;
                }
                that.setData({
                    spinners: temps,
                })
            },
        
            spinnerclick(event) {
                const that = this;
                that.setData({
                    showspinner: false,
                    selectedNav : '00'
                })
            }
```

## 查询框
wxml中
```
  <view class='search'>
    <icon type="search" color="#4c4c4c" size="18"></icon>
    <input type="text" maxlength="100" placeholder="输入商户名、地名、找优惠" placeholder-style="color:#999999" />
  </view>
```
wxss中
```
page{
    background-color: #f0f0f0;
}
.search{
    background-color: #fff;
    margin: 20rpx 40rpx;
    border-radius: 70rpx;
    height: 70rpx;
    line-height: 70rpx;
    display: flex;
    flex-wrap: nowrap;
    padding: 0 30rpx;
    vertical-align: middle;
    align-items: center;
}

.search icon{
margin-right: 10rpx;
height: 18px;
}
.search input{
    flex: 1;
    vertical-align: middle;
    height: 70rpx;
      display: inline-block;
      font-size: 26rpx;
}
```

## 评星控件
wxml中
```
<import src="../../components/star/star.wxml"/>
<template is="star" data="{{count:3.8}}"/>
```
star.wxml中
```
<template name='star'>
  <view class='star-rating'>
    <block wx:for="{{[1,2,3,4,5]}}" wx:for-item='i' wx:key='*this'>
      <image src="../../images/arrow01.png" wx:if="{{i <= count}}"></image>
      <image src="../../images/arrow02.png" wx:if="{{ i > count && i - 1 < count }}"></image>
      <image src="../../images/arrow03.png" wx:if="{{ i > count && !(i - 1 < count) }}"></image>
    </block>
  </view>
</template>
```
注意，需要传count参数
star.wxss中
```
.star-rating{
    display: inline-block;
    margin-right: 6rpx;
}
.star-rating image{
      width: 28rpx;
      height: 27rpx;
      margin-right: 4rpx;
}
```