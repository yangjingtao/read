# rem适配

#### 在介绍它的做法之前，先来了解一点关于viewport的知识，通常我们采用如下代码设置viewport:

        <meta name="viewport"   content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no">

        这样整个网页在设备内显示时的页面宽度就会等于设备逻辑像素大小，也就是device-width。这个device-width的计算公式为：

        设备的物理分辨率/(devicePixelRatio * scale)，在scale为1的情况下，device-width = 设备的物理分辨率/devicePixelRatio

1. 通过js设置viewport的方法如下：

    var scale = 1 / devicePixelRatio;

    document.querySelector(‘meta[name="viewport"]‘.setAttribute(‘content‘,‘initial-scale=‘ + scale + ‘, maximum-scale=‘ + scale + ‘, minimum-scale=‘ + scale + ‘, user-scalable=no‘);

2. html元素的font-size的计算公式，font-size = deviceWidth / 10：

    接下来要解决的问题是，元素的尺寸该如何计算，比如说设计稿上某一个元素的宽为150px，换算成rem应该怎么算呢？这个值等于设计稿标注尺寸/该设计稿对应的html的font-size。拿淘宝来说的，他们用的设计稿是750的，所以html的font-size就是75，如果某个元素时150px的宽，换算成rem就是150 / 75 = 2rem。

     @1: 动态设置viewport的scale

        var scale = 1 / devicePixelRatio;

        document.querySelector(‘meta[name="viewport"]‘).setAttribute(‘content‘,‘initial-scale=‘ + scale + ‘, maximum-scale=‘ + scale + ‘, minimum-scale=‘ + scale + ‘, user-scalable=no‘)


     @2: 动态计算html的font-size

        document.documentElement.style.fontSize = document.documentElement.clientWidth / 10 + ‘px‘;

     @3: 布局的时候，各元素的css尺寸=设计稿标注尺寸/设计稿横向分辨率/10

     @4: font-size可能需要额外的媒介查询，并且font-size不使用rem。


### less


1. //定义一个变量和一个mixin

        @baseFontSize: 75;//基于视觉稿横屏尺寸/100得出的基准font-size
        .px2rem(@name, @px){
            @{name}: @px / @baseFontSize * 1rem;
        }

2. //使用示例：

        .container {
            .px2rem(height, 240);
        }

3. less翻译结果：

        .container {
            height: 3.2rem;
        }

