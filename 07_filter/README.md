#过滤器
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

##7.1 过滤器currency
currecy过滤器可以将一个数值格式化为货币格式,默认情况下会采用客户端所处区域的货币符号, 也可以自定义货币符号。
例如:```{{ 123 | currency }}```

##7.2
