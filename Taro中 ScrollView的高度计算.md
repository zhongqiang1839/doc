
> 在taro中,编译时Taro会帮你做尺寸转换，所以你scss中写的 100px 会自动帮你转换成相应的rem，but如果你在js中书写了行内样式，Taro就无能无力了，既然内联写calc(100vh - 100px)Taro并不会帮我们转换，针对这种情况:


官方 Taro 提供了 API Taro.pxTransform 来做运行时的尺寸转换。

```javascript
  Taro.pxTransform(10) // 小程序（微信，支付宝）：rpx，H5：rem
```

已知我们自己的项目中使用了px作为单位，Taro 默认以 750px 作为换算尺寸标准 so, 有以下两种方案：

1. 通过添加class去处理，当然是可以行的，缺点也很明显，必须已知 topNav。 比较局限并不通用。

代码如下：

```javascript

  const { hasTopNav } = this.props

  <ScrollView 
    className={`demo ${hasTopNav ? 'demo__high' : ''}`}
    scrollY 
    onScrollToLower={onGetMore} 
    lowerThreshold='100' 
    scrollTop={scrollTop}
  >
  
  </ScrollView>
 
```

```css
   
   .demo {
     height: 100vh;
     
     &__high {
        height: calc(100vh - 20px)
     }
             
   } 
```

2. 如果要用在组件里面，topNav 高度未知， 是通过调用组件的方式传入， 就比较通用了。**（height * 2）** 是什么鬼???  因为上面讲到 Taro.pxTransform 会将你的高度转换成 rpx， 已知1px = 2rpx。而且我们用px单位。 所我们传给组件的值需要 *2 ，到这就完了。height是不带单位的。

代码如下：


```javascript

  const { height = 0 } = this.props
  
  <ScrollView 
    className=’demo‘
    style={`height: calc(100vh - ${Taro.pxTransform(height * 2)})`}
    scrollY 
    onScrollToLower={onGetMore} 
    lowerThreshold='100' 
    scrollTop={scrollTop}
  >
  
  </ScrollView>
 
```

>如果已知 height = 40， ${Taro.pxTransform(height * 2)} = ？
>在iphone5下等于 34px
>在iphone6，7，X下均等于 40px



* * *


> 总结: 什么时候Taro内联的样式也能转换，就不要做这么多了。
