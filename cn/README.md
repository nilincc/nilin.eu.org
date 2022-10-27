# 足迹地图

> 给你的博客和网站加上自己的足迹地图吧，世界很大，一定要去看看。



# 百度AK获取

在[百度地图开放平台](https://lbsyun.baidu.com/)注册一个开发者身份认证（基本秒过）

![](https://s1.vika.cn/space/2022/10/27/e355736558a24732982cee3286561d47)

创建一个新的应用，应用名称随意填写，应用类型选择浏览器端，白名单填写你的域名或者ip，测试阶段可以用*代替，创建成功会得到一个访问AK。

![](https://s1.vika.cn/space/2022/10/27/59b5e66b267b473692c899b0109b2870)

![](https://s1.vika.cn/space/2022/10/27/b164930d7c4e4532bc1b726485c24986)

# 源码

```html
<!DOCTYPE html>
<html>

<head>
    <meta name="viewport" content="initial-scale=1.0, user-scalable=no" />
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
    <title>Hello, World</title>
    <style type="text/css">
        html {
            height: 100%
        }

        body {
            height: 100%;
            margin: 0px;
            padding: 0px
        }

        #container {
            height: 100%
        }
    </style>
    <script type="text/javascript" src="https://api.map.baidu.com/api?v=1.0&type=webgl&ak=你的AK">
    </script>
</head>

<body>
    <div id="container"></div>
    <script type="text/javascript">
        var map = new BMapGL.Map("container");// 创建地图实例 
        var point = new BMapGL.Point(105.59123, 30.548022);// 创建点坐标，打开页面中心点
        map.centerAndZoom(point, 6);// 初始化地图，设置中心点坐标和地图级别 
        map.enableScrollWheelZoom(true); //启用滚轮放大缩小
        map.setMapStyleV2({
            styleId: '样式ID'
        });//地图样式


        const markeArray = [
            {
                longitude: 118.4308,  //经度
                latitude: 31.3543,    //纬度
                richText: `<h4 style='margin:0 0 6px 0;'>芜湖</h4> 2019.4.5点亮
                        <img style='float:right;margin:0 2px 11px' id='imgDemo' src='图片URL' width='139' height='104'/>
                        <p style='margin:0;line-height:1.5;font-size:13px;text-indent:2em'>
                        地址：地处中国华东地区，安徽省东南部，西汉武帝元封二年前置县，因“蓄水不深而多生芜藻”始名“芜湖”。
                        </p>`
            },

            {
                longitude: 104.0601,  //经度
                latitude: 30.5994,    //纬度
                richText: `<h4 style='margin:0 0 6px 0;'>成都</h4> 2001.2.1点亮
                        <img style='float:right;margin:0 2px 11px' id='imgDemo' src='图片URL' width='139' height='104'/>
                        <p style='margin:0;line-height:1.5;font-size:13px;text-indent:2em'>
                        地址：位于中国四川省中部，为四川省省会，国家中心城市。
                        </p>`
            },
        ];

        markeArray.forEach(item => {
            let marker1 = new BMapGL.Marker(new BMapGL.Point(item.longitude, item.latitude));// 创建点标记

            map.addOverlay(marker1);// 在地图上添加点标记
            // 创建信息窗口
            var opts = {
                width: 50,
                height: 25,
                title: item.title,
            };
            var infoWindow = new BMapGL.InfoWindow(item.richText);
            // 点标记添加点击事件
            marker1.addEventListener('click', function () {
                map.openInfoWindow(infoWindow, new BMapGL.Point(item.longitude, item.latitude)); // 开启信息窗口
            });

        });
    </script>
</body>

</html>
```

# 如何嵌入到网页

```
<iframe style="max-width: 100%" frameborder="no" border="0" marginwidth="0" marginheight="0" width="100%" height="750px"src="替换成你的足迹地图链接"></iframe>
```

------

原文链接：[使用百度地图API制作个人足迹地图 - 关山映月 (koko.cx)](https://koko.cx/notes/baidumap.html)
