#模块
- 模块定义了一个应用程序。
- 模块是应用程序中不同部分的容器。
- 模块是应用控制器的容器。
- 控制器通常属于一个模块。
AngularJS模块（Module）定义了AngularJS 应用。

AngularJS 控制器（Controller）用于控制 AngularJS 应用。

ng-app指令定义了应用, ng-controller 定义了控制器。

```
<!doctype html>
<html>
<body>
<div ng-app="myApp" ng-controller="myController">
    <input type="text" ng-model="username"/>
    {{username||"null"}}
</div>
<script src="https://cdn.bootcss.com/angular.js/1.2.29/angular.min.js"></script>
<script>
    var app=angular.module("myApp",[]);
    app.controller("myController",function($scope){
        $scope.username="China";
    });
</script>
</body>
</html>
```

