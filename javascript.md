##  获取浏览器版本信息的方法

        navigator.userAgent；
        navigator.appName--官方浏览器名的字符串表示
        navigator.appVersion--浏览器版本信息的字符串表示
        navigator.cookieEnabled--如果启用cookie返回true，否则返回false

##  类数组转化数组

        Array.proptype.slice.call(arguments);

##  解决chrome下字体小于12px

        1. -webkit-text-size-adjust：none；
        2. -webkit-transform：scale（0.75）



##  如何判断数组类型
1.  instanceof
    var a=[];
    console.log(a instanceof Array) //返回true

2.  constructor
    var a=[];
    console.log(a.constructor == Array);

3.  isArray

```
function isArray(object){
    return object && typeof object==='object' &&
            Array == object.constructor;
}
```

##  HTML

###  global对象

1.  isNaN();

2.  isFinite();

3.  parseInt();

4.  parseFloat();

5.  encodeURL()-----decodeURL();

6.  encodeURLComponent()-----decodeURLComponent();


