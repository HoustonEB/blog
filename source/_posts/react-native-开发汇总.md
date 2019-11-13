---
title: react-native 开发汇总
date: 2019-10-29 10:20:15
categories: react-native
tags:
- react-native
---
## 标签

1.View
2.Text
3.ScrollView
- showsHorizontalScrollIndicator: 隐藏水平滚动条

4.RefreshControl
- refreshing: 是否显示刷新器
- onRefresh: 当滚动距离顶部距离0,触发函数
- progressBackgroundColor: loading背景色(Android)
- tintColor: 刷新器(圈圈)的颜色(iOS)
- size: 刷新器的大小0大1小
- title: 再刷新器下显示的文字(iOS)
- titleColor: 刷新起下文字的颜色(iOS)
- progressViewOffset: 刷新起距离上部的距离(Android)
- 添加上拉刷新
<--! more -->
```html
<ScrollView
        style={styles.scrollview}
        refreshControl={
          <RefreshControl
            refreshing={this.state.isRefreshing}
            onRefresh={this._onRefresh}
            tintColor="#ff0000"
            title="Loading..."
            titleColor="#00ff00"
            colors={['#ff0000', '#00ff00', '#0000ff']}
            progressBackgroundColor="#ffff00"
          />
        }>
        {rows}
      </ScrollView>
```

5.TouchableOpacity
用来封装自己的Button,因为Button没有触摸的反馈效果.
- onPress: 触摸触发的函数
- activeOpacity: 指定封装的视图在被触摸操作激活时以多少不透明度显示（通常在0到1之间）.
6.WebView
- 已被rn移除,改用[react-native-webview](https://github.com/react-native-community/react-native-webview)
---
## 导航器

1.react-navigation
- StackNavigator - 为应用程序提供了一种切换的方法,每次切换时,新的页面会放置再堆栈的顶部
- TabNavigator - 用于设置具有多个Tab页的页面
- DrawerNavigator - 用于设置抽屉导航的页面

## 轮播图
1.react-native-swiper
> v1.5.14
`npm i react-native-swiper --save`
> v1.6.0-nightly
`npm i --save react-native-swiper@nightly`
安装v1.5.14版本会报错,因为rn高版本移除了<ViewPagerAndroid />,而swipper依赖于它.
v1.6.0替换掉了这个标签.
