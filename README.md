# 微信小程序的相关操作

* [页面跳转](#页面跳转)
* [banner的显示](#banner的显示)
* [多个图片横向排列多行](#多个图片横向排列多行)
* [列表显示](#列表显示)
* [下拉列表](#下拉列表)
* [查询框](#查询框)
* [评星控件](#评星控件)
* [分类中的列表显示](#分类中的列表显示)
* [下方弹出选择框](#下方弹出选择框)
* [起始页闪屏](#起始页闪屏)
* [侧边栏](#侧边栏)
* [抽奖](#抽奖)
* [多张图片横向排列单行](#多张图片横向排列单行)


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

## 多个图片横向排列多行
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

## 分类中的列表显示
wxml中
```
    <view class="select-item">
      <view class="select-title">大家都在搜</view>
      <view class="select-iconList one-iconList">
        <navigator class="select-iconitem" wx:for="{{searchNameArr.searchOne}}" data-id="{{item.id}}" url="/pages/searchList/searchList?keywordsId={{item.id}}" hover-class="navigator-hover">{{item.keywords}}</navigator>
      </view>
    </view>
```
wxss中
```
.select-item{
  width:100%;
}
.select-title{
  width:100%;
  text-align: center;
  padding:20rpx 0;
}
.select-iconList{
  width:100%;
  height:210rpx;
  text-align: center;
  overflow: hidden;
}
.select-iconitem{
  margin:14rpx;
  /* margin-bottom:20rpx; */
  padding:0 30rpx;
  height:70rpx;
  line-height: 70rpx;
  box-sizing: border-box;
  border-radius: 70rpx;
  color:#7ac873;
  border: 1px solid #7ac873;
  display:inline-block;
}

.one-iconList navigator{
  color:#7ac873;
   border: 1px solid #7ac873;
}
```
js中
```
    searchNameArr:
        {
            searchOne:[
                {
                    id:1,
                    keywords:'年夜饭'
                },
                {
                    id: 1,
                    keywords: '热门菜谱榜'
                },
                {
                    id: 1,
                    keywords: '汤'
                },
                {
                    id: 1,
                    keywords: '蛋糕'
                },
                {
                    id: 1,
                    keywords: '早餐'
                },
                {
                    id: 1,
                    keywords: '豆腐'
                }
            ]
        }
```

## 下方弹出选择框
wxml中
```
    <view class="userdata">
      <view class="userdata-name">星座</view>
      <view class="userdata-symbol"></view>
      <picker mode="selector" class="userdata-input" range="{{actionConItems}}" value="{{conIndex}}" bindchange="pickerConSelected">
           <text>{{actionConItems[conIndex]}}</text>
      </picker>
      <text class="righthead"></text>
    </view>
```
wxss中
```
.userdata {
  margin: 10rpx 0rpx;
  border: 1rpx solid #6c6c6c;
  width: 90%;
  display: flex;
  flex-direction: row;
  border-radius: 10rpx;
  align-items: center;

}
.userdata-name {
  padding: 30rpx 30rpx;
}
/*第一个箭头*/
.userdata-symbol:after {
  content: "";
  display: inline-block;
  width: 40rpx;
  height: 40rpx;
  margin: 15rpx 0rpx 10rpx 0rpx;
  border-left: 1rpx solid #6c6c6c;
}
/*后面三个箭头*/
.userdata-input {
  width: 300rpx;
}

.righthead:after {
  content: '';
  /*即不把兄弟挤下去 又能设置自己的style  inline不能设置大小 block会挤下去 所以有了inline-block*/
  display: inline-block;
  width: 18rpx;
  height: 18rpx;
  border: 3rpx solid #A9A9A9;
  border-bottom: none;
  border-left: none;
  transform: rotate(45deg);
  margin-left: 160rpx;
}
```
js中
```
  data:{
    actionConItems: ['白羊座', '金牛座', '双子座', '巨蟹座', '狮子座', '处女座', '天秤座', '天蝎座', '射手座', '摩羯座', '水瓶座', '双鱼座'],
    conIndex: 0,
  },
  //星座弹出窗口  可以将数据放在本地setStorage
  pickerConSelected: function (e) {
    console.log('picker发送选择改变，星座为' + e.detail.value);
    wx.setStorageSync("con", e.detail.value);
    this.setData({
      conIndex: e.detail.value,
      btnColor: "#ffc324",
    });
  },
  onLoad: function (options) {
    //这里是本地的信息获取
    if (wx.getStorageSync("con") !== '') {
      this.setData({
        conIndex: wx.getStorageSync("con")
      })
    }
  }
```

## 起始页闪屏
wxml中
```
<view class="logo">
  <image bindtap="bindLogoTap" class="logo_page" src="/images/logo.jpg" mode="widthFix"></image>
</view>
```
wxss中
```
.logo_page {
    width: 100%;
    height:100vh;
}
```
js中
```
Page({
  data: {
    time: 2,
    jump:false
  },

  bindLogoTap: function () {
    wx.switchTab ({
      url: '../index/index'
    });
    this.setData({jump:true})
  },
  /**
   * 生命周期函数--监听页面加载
   */
  onLoad: function (options) {
    // 设置初始计时秒数
    let time = 2;
    // 开始定时器
    this.timer = setInterval(() => {
      this.setData({
        time: --time
      });
      // 读完秒后携带洗衣机编号跳转到计费页
      if (time < 0) {
        clearInterval(this.timer)
        if (!this.data.jump) {
          wx.switchTab({
            url: '../index/index'
          })
        }
      }
    }, 1000)
  }
})
```
需要注意的是跳转的如果是正常页面可以redirectTo方法，但是如果跳转的是tabBar，则需要调用switchTab方法  

## 侧边栏
wxml中
```
<view class="page-bottom {{showPageBottom?'active':''}}">
</view>
<view class="img-content {{showPageBottom?'active':''}}">
  <image bindtap="showMenu" src="../../images/btn.png"></image>
</view>
```
wxss中
```
.page-bottom {
    height: 100%;
    width: 500rpx;
    position: fixed; 
    background-color: white;
    z-index: 9999;  
    transform: translateX(-100%);
    transition: transform .5s;
    /*设置元素的堆叠顺序,拥有更高堆叠顺序的元素总是会处于堆叠顺序较低的元素的前面，
    元素可拥有负的 z-index 属性值。Z-index 仅能在定位元素上奏效如position:absolute;*/
}
.page-bottom.active {
    transform: translateX(0%);
}
.img-content {
    position: absolute; 
    width: 100%;
    padding-top: 0rpx;
    transition: all .5s; 
    transform: translateX(0%);
}

.img-content.active {
    transform: translateX(65%);
}
```
js中
```
    data: {
        showPageBottom: false
    },

    
    showMenu: function() {
        this.setData({
            showPageBottom: !this.data.showPageBottom
        })
    }
```

## 抽奖
wxml中
```
		<view class="canvas-container">
			<view  animation="{{animationData}}" class="canvas-content" >
				<canvas style="width: 300px; height: 300px;" class="canvas-element" canvas-id="lotteryCanvas"></canvas>

				<view class="canvas-line">
					<view class="canvas-litem" wx:for="{{awardsList}}" wx:key="unique" style="-webkit-transform: rotate({{item.lineTurn}});transform: rotate({{item.lineTurn}})"></view>
				</view>

				<view class="canvas-list">
					<view class="canvas-item" wx:for="{{awardsList}}" wx:key="unique">
				  		<view class="canvas-item-text" style="-webkit-transform: rotate({{item.turn}});transform: rotate({{item.turn}})">{{item.award}}</view>
					</view>
				</view>

				
			</view>

			<view bindtap="getLottery" class="canvas-btn {{btnDisabled}}">抽奖</view>		
		</view>
```
wxss中
```
/* 转盘 */
.canvas-container ul,
.canvas-container li{
  margin: 0 ;
  padding: 0;
  list-style: none;
}

.canvas-container{
  margin: 0 auto;
  position: relative;
  width: 300px;
  height: 300px;  
  border-radius: 50%;
  /*border: 2px solid #E44025;*/
  box-shadow: 0 2px 3px #333,
              0 0 2px #000;
}
.canvas-content{
  position: absolute;
  left: 0;
  top: 0;
  z-index: 1;
  display: block;
  width: 300px;
  height: 300px;
  border-radius: inherit;
  background-clip: padding-box;
  background-color: #ffcb3f;
}
.canvas-element{
  position: relative;
  z-index: 1;
  width: inherit;
  height: inherit;
  border-radius: 50%;
}
.canvas-list{
  position: absolute;
  left: 0;
  top: 0;
  width: inherit;
  height: inherit;
  z-index: 9999;
}
.canvas-item{
  position: absolute;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  color: #e4370e;
  font-weight: bold;
  text-shadow: 0 1px 1px rgba(255,255,255,.6);
}
.canvas-item-text{
  position: relative;
  display: block;
  padding-top: 20px;
  /* width: 50px; */
  margin: 0 auto;
  text-align: center; 
  -webkit-transform-origin: 50% 150px; 
  transform-origin: 50% 150px;
}

/* 分隔线 */
.canvas-line{
  position: absolute;
  left: 0;
  top: 0;
  width: inherit;
  height: inherit;
  z-index: 99;
}
.canvas-litem{
  position: absolute;
   left: 150px;
   top: 0;
   width: 1px;
   height: 150px;
   background-color: rgba(228,55,14,.4);
   overflow: hidden; 
   -webkit-transform-origin: 50% 150px; 
   transform-origin: 50% 150px;
}


.canvas-btn{
  position: absolute;
  left: 110px;
  top: 110px;
  z-index: 400;
  width: 80px;
  height: 80px;
  border-radius: 50%;
  color: #F4E9CC;
  background-color: #E44025;
  line-height: 80px;
  text-align: center;
  font-size: 20px;
  text-shadow: 0 -1px 1px rgba(0,0,0,.6);
  box-shadow: 0 3px 5px rgba(0,0,0,.6);
  text-decoration: none;
}
.canvas-btn::after{
  position: absolute;
  display: block;
  content: ' ';
  left: 10px;
  top: -46px;
  width: 0;
  height: 0;
  overflow: hidden;
  border-width: 30px;
  border-style: solid;
  border-color: transparent;
  border-bottom-color: #E44025; 
}
.canvas-btn.disabled{
    pointer-events: none;
    background: #B07A7B;
    color: #ccc;
}
.canvas-btn.disabled::after{
  border-bottom-color: #B07A7B;
}
```
js中
```
  data: {
    awardsList: {},
    animationData: {},
    btnDisabled: ''
  },
  getLottery: function () {
    var that = this
    var awardIndex = Math.random() * 6 >>> 0;

    // 获取奖品配置
    var awardsConfig = app.awardsConfig,
        runNum = 8
    if (awardIndex < 2) awardsConfig.chance = false
    console.log(awardIndex)

    // 初始化 rotate
  /*  var animationInit = wx.createAnimation({
      duration: 10
    })
    this.animationInit = animationInit;
    animationInit.rotate(0).step()
    this.setData({
      animationData: animationInit.export(),
      btnDisabled: 'disabled'
    })*/

    // 旋转抽奖
    app.runDegs = app.runDegs || 0
    console.log('deg', app.runDegs)
    app.runDegs = app.runDegs + (360 - app.runDegs % 360) + (360 * runNum - awardIndex * (360 / 6))
    console.log('deg', app.runDegs)

    var animationRun = wx.createAnimation({
      duration: 4000,
      timingFunction: 'ease'
    })
    that.animationRun = animationRun
    animationRun.rotate(app.runDegs).step()
    that.setData({
      animationData: animationRun.export(),
      btnDisabled: 'disabled'
    })

     // 记录奖品
    var winAwards = wx.getStorageSync('winAwards') || {data:[]}
    winAwards.data.push(awardsConfig.awards[awardIndex].name + '1个')
    wx.setStorageSync('winAwards', winAwards)

    // 中奖提示
    setTimeout(function() {
      wx.showModal({
        title: '恭喜',
        content: '获得' + (awardsConfig.awards[awardIndex].name),
        showCancel: false
      })
      if (awardsConfig.chance) {
        that.setData({
          btnDisabled: ''
        })  
      }
    }, 4000);
    

    /*wx.request({
      url: '../../data/getLottery.json',
      data: {},
      header: {
          'Content-Type': 'application/json'
      },
      success: function(data) {
        console.log(data)
      },
      fail: function(error) {
        console.log(error)
        wx.showModal({
          title: '抱歉',
          content: '网络异常，请重试',
          showCancel: false
        })
      }
    })*/
  },
  onReady: function (e) {

    var that = this;

    // getAwardsConfig
    app.awardsConfig = {
      chance: true,
      awards:[
        {'index': 0, 'name': '1元红包'},
        {'index': 1, 'name': '5元话费'},
        {'index': 2, 'name': '6元红包'},
        {'index': 3, 'name': '8元红包'},
        {'index': 4, 'name': '10元话费'},
        {'index': 5, 'name': '10元红包'}
      ]
    }
    
    // wx.setStorageSync('awardsConfig', JSON.stringify(awardsConfig))
    

    // 绘制转盘
    var awardsConfig = app.awardsConfig.awards,
        len = awardsConfig.length,
        rotateDeg = 360 / len / 2 + 90,
        html = [],
        turnNum = 1 / len  // 文字旋转 turn 值
    that.setData({
      btnDisabled: app.awardsConfig.chance ? '' : 'disabled'  
    })
    var ctx = wx.createContext()
    for (var i = 0; i < len; i++) {
      // 保存当前状态
      ctx.save();
      // 开始一条新路径
      ctx.beginPath();
      // 位移到圆心，下面需要围绕圆心旋转
      ctx.translate(150, 150);
      // 从(0, 0)坐标开始定义一条新的子路径
      ctx.moveTo(0, 0);
      // 旋转弧度,需将角度转换为弧度,使用 degrees * Math.PI/180 公式进行计算。
      ctx.rotate((360 / len * i - rotateDeg) * Math.PI/180);
      // 绘制圆弧
      ctx.arc(0, 0, 150, 0,  2 * Math.PI / len, false);

      // 颜色间隔
      if (i % 2 == 0) {
          ctx.setFillStyle('rgba(255,184,32,.1)');
      }else{
          ctx.setFillStyle('rgba(255,203,63,.1)');
      }

      // 填充扇形
      ctx.fill();
      // 绘制边框
      ctx.setLineWidth(0.5);
      ctx.setStrokeStyle('rgba(228,55,14,.1)');
      ctx.stroke();

      // 恢复前一个状态
      ctx.restore();

      // 奖项列表
      html.push({turn: i * turnNum + 'turn', lineTurn: i * turnNum + turnNum / 2 + 'turn', award: awardsConfig[i].name});    
    }
    that.setData({
        awardsList: html
      });

    // 对 canvas 支持度太差，换种方式实现
    /*wx.drawCanvas({
      canvasId: 'lotteryCanvas',
      actions: ctx.getActions()
    })*/
  }
```

## 多张图片横向排列单行
wxml中
```
<view class="section section_gap">
  <view class="section__title">三亚热拍</view>
  <scroll-view class="scroll-view_H" scroll-x="true">
    <view class="scroll-view-item_H" wx:for="{{hotList}}" wx:key="{{item}}" data-pic="{{item.pic}}"
    data-title="{{item.title}}" data-area="{{item.area}}" data-day="{{item.day}}" data-avatar="{{item.avatar}}"
    data-name="{{item.name}}" data-fee="{{item.fee}}"  data-experience="{{item.experience}}" bindtap="yuyue">
      <image src="{{item.pic}}"class="scroll-image"/>
      <view class="content">
      <view  class="title" >{{item.title}}</view>
      <view class="scroll-view-item-AT">
        <view class="area">{{item.area}}</view>
        <view class="day">{{item.day}}</view>
      </view>
      <view class="scroll-view-item-cf">
        <view class="camerist_avatar"><image src="{{item.avatar}}"></image></view>
        <view class="camerist_name">{{item.name}}</view>
        <view class="fee">{{item.fee}}</view>
      </view>
      </view>
    </view>
  </scroll-view>
</view>
```
wxss中
```
.section{
  width: 100%;
  height: 580rpx;
}
.section__title{
  padding-top: 12rpx;
  width:100%;
  height:80rpx;
  line-height:80rpx;
  position: relative;
  text-align: center;
  font-size: 50rpx;
  color:#A9A9A9;
  font-weight: bold;
}
.section__title::before{
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 12rpx;
  background:#FFEFDB;
}
.scroll-view_H{
  height:500rpx;
  white-space: nowrap;
  display: flex;

}
.scroll-view-item_H{
  width:340rpx;
  height:500rpx;
  margin-right: 24rpx;
  display: inline-block;

}
.scroll-image{
  width:340rpx;
  height:300rpx;
  display: block;
}
.scroll-view-item_H .content{
  width: 338rpx;
  height: 190rpx;
  border: 1rpx solid #FFEFDB;
}
.title{
  margin-top: 20rpx;
  height:40rpx;
  line-height:40rpx;
  font-size: 30rpx;
  text-align: center;
  font-weight: 400;
  color:#A8A8A8;
}
.scroll-view-item-AT{
  margin-top: 20rpx;
  width: 100%;
  height: 40rpx;
  font-size: 11px;
  color:#A8A8A8;

}
.area{
  float: left;
  width: 60rpx;
  height: 30rpx;
  line-height: 30rpx;
}
.day{
  float:left;
  width: 60rpx;
  height: 30rpx;
  line-height: 30rpx;
}
.scroll-view-item-cf{
  width: 100%;
  height: 50rpx;
  line-height: 50rpx;
  font-size: 26rpx;
  color:#A8A8A8;
}
.camerist_avatar{
  float: left;
  width: 40rpx;
  height: 40rpx;
  border-radius: 50%;
  vertical-align: middle;
}
.camerist_avatar image{
  width: 40rpx;
  height: 40rpx;
  border-radius: 50%;
  vertical-align: middle;
}
.camerist_name{
  float: left;
  margin-left: 20rpx;
  width: 50rpx;
  height: 50rpx;
  line-height: 50rpx;
  vertical-align: middle;
  font-size: 28rpx;

}
.fee{
  float: right;
  width: 100rpx;
  height: 50rpx;
  line-height: 50rpx;
  font-size: 28rpx;
}
```
js中
```
    hotList:[
      {
        pic:"http://www.lemontreevip.com/upload/201512/201512191450513761.jpg",
        title:"春风十里不如你",
        area:"三亚",
        day:"1day",
        avatar:"http://img3.imgtn.bdimg.com/it/u=4293197616,2435113501&fm=23&gp=0.jpg",
        name:"南若北",
        fee:"3000",
        experience:'7年'
      },
      {
        pic:"http://www.lemontreevip.com/upload/201512/201512191450512739.jpg",
        title:"一场没有终点的旅行",
        area:"三亚",
        day:"1day",
        avatar:"http://img.qq745.com/uploads/allimg/170413/14-1F413113106-53.png",
        name:"苏晓",
        fee:"4000",
        experience:'10年以上'
      },
      {
        pic:"http://www.lemontreevip.com/upload/201603/1458298749772440744000.jpg",
        title:"恋上彩虹的梦",
        area:"三亚",
        day:"1day",
        avatar:"http://img.qq745.com/uploads/allimg/170413/14-1F413113108-52.png",
        name:"峰方",
        fee:"3500",
        experience:'10年'
      },
      {
        pic:"http://www.lemontreevip.com/upload/201512/201512101449733988.jpg",
        title:"日暮三亚",
        area:"三亚",
        day:"1day",
        avatar:"http://img.qq745.com/uploads/allimg/170413/14-1F413113109-52.png",
        name:"大鹏",
        fee:"2500",
        experience:'7年'
      },
      {
        pic:"http://www.lemontreevip.com/upload/201508/1438966134523121267000.jpg",
        title:"帆船高尔夫",
        area:"三亚",
        day:"1day",
        avatar:"http://img.qq745.com/uploads/allimg/170413/14-1F413113111-50.png",
        name:"一方",
        fee:"2500",
        experience:'7年'
      },
      {
        pic:"http://www.lemontreevip.com/upload/201603/201603181458295704.jpg",
        title:"西岛恋曲",
        area:"三亚",
        day:"1day",
        avatar:"http://img.qq745.com/uploads/allimg/150307/1-15030G54010.jpg",
        name:"大浦",
        fee:"1800",
        experience:'5年'
      }
    ],
```