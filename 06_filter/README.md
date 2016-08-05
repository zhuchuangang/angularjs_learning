#6.过滤器
>在HTML中的模板绑定符号{{ }}内通过|符号来调用过滤器。可以用|符号作为分割符来同时使用多个过滤器。

例如:```{{name|uppercase}}```转成大写

>在JavaScript代码中可以通过$filter来调用过滤器。

例如:
```
    var app=angular.module("myApp",[]);
    app.controller("myController",function($scope,$filter){
        $scope.username=$filter("uppercase")("Test");
    });

```

##6.1 过滤器currency
currecy过滤器可以将一个数值格式化为货币格式,默认情况下会采用客户端所处区域的货币符号, 也可以自定义货币符号。
例如:```{{ 123 | currency }}```

##6.2 过滤器date
date过滤器可以将日期格式化成需要的格式。

下面是内置的支持本地化的日期格式:
```
{{ today | date:'medium' }} <!-- Aug 09, 2013 12:09:02 PM -->
{{ today | date:'short' }} <!-- 8/9/1312:09PM -->
{{ today | date:'fullDate' }} <!-- Thursday, August 09, 2013 -->
{{ today | date:'longDate' }} <!-- August 09, 2013 -->
{{ today | date:'mediumDate' }}<!-- Aug 09, 2013 -->
{{ today | date:'shortDate' }} <!-- 8/9/13 -->
{{ today | date:'mediumTime' }}<!-- 12:09:02 PM -->
{{ today | date:'shortTime' }} <!-- 12:09 PM -->
```
年份格式化
```
四位年份:{{ today | date:'yyyy' }} <!-- 2013 -->
两位年份:{{ today | date:'yy' }} <!-- 13 -->
一位年份:{{ today | date:'y' }} <!-- 2013 -->
```
月份格式化
```
英文月份:{{ today | date:'MMMM' }} <!-- August -->
英文月份简写:{{ today | date:'MMM' }} <!-- Aug -->
数字月份:{{ today |date:'MM' }} <!-- 08 -->
一年中的第几个月份:{{ today |date:'M' }} <!-- 8 -->
```
日期格式化
```
数字日期:{{ today|date:'dd' }} <!-- 09 -->
一个月中的第几天:{{ today | date:'d' }} <!-- 9 -->
英文星期:{{ today | date:'EEEE' }} <!-- Thursday -->
英文星期简写:{{ today | date:'EEE' }} <!-- Thu -->
```
小时格式化
```
24小时制数字小时:{{today|date:'HH'}} <!--00-->
一天中的第几个小时:{{today|date:'H'}} <!--0-->
12小时制数字小时:{{today|date:'hh'}} <!--12-->
上午或下午的第几个小时:{{today|date:'h'}} <!--12-->
```
分钟格式化
```
数字分钟数:{{ today | date:'mm' }} <!-- 09 -->
一个小时中的第几分钟:{{ today | date:'m' }} <!-- 9 -->
```

秒数格式化
```
数字秒数:{{ today | date:'ss' }} <!-- 02 -->
一分钟内的第几秒:{{ today | date:'s' }} <!-- 2 -->
毫秒数:{{ today | date:'.sss' }} <!-- .995 -->
```

字符格式化
```
上下午标识:{{ today | date:'a' }} <!-- AM -->
四位时区标识:{{ today | date:'Z' }} <!--- 0700 -->
```

下面是一些自定义日期格式的示例:
```
{{ today | date:'MMMd, y' }} <!-- Aug9, 2013 -->
{{ today | date:'EEEE, d, M' }} <!-- Thursday, 9, 8-->
{{ today | date:'hh:mm:ss.sss' }} <!-- 12:09:02.995 -->
```

##6.3 过滤器filter
filter过滤器可以从给定数组中选择一个子集,并将其生成一个新数组返回。

- 字符串
返回所有包含这个字符串的元素。如果我们想返回不包含该字符串的元素,在参数前加!符号。

- 对象
AngularJS会将待过滤对象的属性同这个对象中的同名属性进行比较,如果属性值是字符串就会判断是否包含该字符串。
如果我们希望对全部属性都进行对比,可以将$当作键名。

- 函数
对每个元素都执行这个函数,返回非假值的元素会出现在新的数组中并返回。
例如,用下面的过滤器可以选择所有包含字母e的单词:
```
{{ ['Ari','Lerner','Likes','To','Eat','Pizza'] | filter:'e' }}
<!-- ["Lerner","Likes","Eat"] -->
```

如果要过滤对象,可以使用上面提到的对象过滤器。
例如,如果有一个由people对象组成的 数组,每个对象都含有他们最喜欢吃的食物的列表,那么可以用下面的形式进行过滤:
```
     {{ [{
         'name': 'Ari',
         'City': 'San Francisco',
         'favorite food': 'Pizza'
         },{
         'name': 'Nate',
         'City': 'San Francisco',
         'favorite food': 'indian food'
         }] | filter:{'favorite food': 'Pizza'} }}
<!-- [{"name":"Ari","City":"SanFrancisco","favoritefood":"Pizza"}] -->
```

也可以用自定义函数进行过滤(在这个例子中函数定义在$scope上):
```
{{ ['Ari','likes','to','travel'] | filter:isCapitalized }}
<!-- ["Ari"] -->
```
isCapitalized函数的功能是根据首字母是否为大写返回true或false,具体如下所示:
```
$scope.isCapitalized = function(str) {
    return str[0] == str[0].toUpperCase();
};
```

我们也可以给filter过滤器传入第二个参数,用来指定预期值同实际值进行比较的方式。
第二个参数可以是以下三种情况之一。
true  用angular.equals(expected, actual)对两个值进行严格比较。
false 进行区分大小写的子字符串比较。
函数   运行这个函数,如果返回真值就接受这个元素。