---
title: 三大地图APP的调起（百度，高德，腾讯）
tag: 移动端
---
关于百度地图，高德地图，腾讯地图在H5中的调起方式总结

# 地图APP调起

## 百度地图

贴上百度地图调起的接口地址：https://lbsyun.baidu.com/index.php?title=uri，具体的参数还是以接口文档的为主
在调起百度地图的时候需要在index.html 入口加上需要用到的百度AK，代码如下：
``` js
  <script type="text/javascript" src="//api.map.baidu.com/api?v=2.0&ak=zUGxGhLQjL9rtAdR5S5cGmVrubmfmZfG"></script>  
```
百度地图因当前web版本在苹果系统高版本调起会去到下载页，最终还是考虑APP的scheme协议调起，代码如下所示:

``` js
  static wakeBaidu(urlObject) {
    console.log(urlObject);
    var geolocation = new BMap.Geolocation();
    geolocation.getCurrentPosition(function (result) {
      console.log(result,'result');
      if (this.getStatus() == BMAP_STATUS_SUCCESS) {
        var latCurrent = result.point.lat; //获取到的纬度
        var lngCurrent = result.point.lng; //获取到的经度
        if (latCurrent && lngCurrent) {
          var scheme = '';
          let u = navigator.userAgent;
          const isiOS = !!u.match(/\(i[^;]+;( U;)? CPU.+Mac OS X/); //ios终端
          if (isiOS) {
            // web版本调起
             window.location.href = "http://map.baidu.com/mobile/marker?location=" + urlObject.lat + "," + urlObject.lng + "&title=" + urlObject.name + "&content=" +urlObject.addr+ "&output=html&src=changan|yingxiaobao"
            // ios 端 scheme协议调起 IOS9以上需要APP端配置才可调起成功  location直接定位点击开始导航 direction驾车导航
            // let queryStr = `${urlObject.lat},${urlObject.lng}&title=${urlObject.name}&content=${urlObject.addr}&src=ios.changan.yingxiaobao`;
            // scheme = 'baidumap://map/marker?location=' + queryStr;
            // scheme = `baidumap://map/direction?origin=${latCurrent},${lngCurrent}&destination=${urlObject.lat},${urlObject.lng}&mode=driving&src=webapp.marker.changan.yingxiaobao`
            // console.log(scheme);
            // window.location.href = scheme;
            return;
          } else {
          // android 端
          let queryStr = `${urlObject.lat},${urlObject.lng}&title=${urlObject.name}&content=${urlObject.addr}&traffic=on&src=andr.changan.yingxiaobao`;
            scheme = 'bdapp://map/marker?location=' + queryStr;
            window.location.href = scheme;
          }
        } else {
          console.log('获取不到定位，请检查手机定位设置');
        }
      }
    });
  }
```

## 高德地图

高德地图就简单一些，直接就以下的链接，在配置参数`callnative=1`，即可调起高德地图APP；同样的还是贴上接口地址，方便查看以下的一些参数
地址：https://lbs.amap.com/api/uri-api/guide/mobile-web/point

``` js
        location.href = `https://uri.amap.com/marker?position=${obj.center.split(',')[1]},${obj.center.split(',')[0]}&name=${obj.name}&coordinate=gaode&callnative=1`
```

## 腾讯地图

同样的贴上地址：https://lbs.qq.com/uri_v1/guide-poiMarker.html

``` js
    location.href = `https://apis.map.qq.com/uri/v1/marker?marker=coord:${obj.center};title:${obj.name};addr:${obj.addr}&referer=productName`
```