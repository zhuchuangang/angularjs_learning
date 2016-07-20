#控制器

AngularJS中的控制器是一个函数,用来向视图的作用域中添加额外的功能。我们用它来给作用域对象设置初始状态.

当我们在页面上创建一个新的控制器时,AngularJS会生成并传递一个新的$scope给这个控制器。可以在这个控制器里初始化$scope。由于AngularJS会负责处理控制器的实例化过程,我们只需编写构造函数即可。

## 控制器初始化
```
     function FirstController($scope) {
       $scope.message = "hello";
}
```

> 上面是在全局作用域中创建的FirstController这个函数,会污染全局命名空间。

## 更合理的是在模块中创建控制器
```
 var app = angular.module('app', []);
     app.controller('FirstController', function($scope) {
       $scope.message = "hello";
     });
```

## AngularJS允许我们在视图中像调用普通数据一样调用$scope上的函数

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>root scope</title>
</head>
<body>
<div ng-app="myApp">
    <div ng-controller="myController">
        <button ng-click="add(1)">add</button>
        <button ng-click="subtract(1)">subtract</button>
        count:<input type="text" value="{{count}}"/>
    </div>
</div>
<script src="https://cdn.bootcss.com/angular.js/1.2.29/angular.min.js"></script>
<script type="text/javascript">
    var app = angular.module("myApp",[]);
    app.controller("myController",function($scope){
        $scope.count=0;
        $scope.add=function(value){
            $scope.count+=value;
        }
        $scope.subtract=function(value){
            $scope.count-=value;
        }
    });
</script>
</body>
</html>
```
> AngularJS同其他JavaScript框架最主要的一个区别就是,控制器并不适合用来执行DOM操作、格式化或数据操作,以及除存储数据模型之外的状态维护操作。它只是视图和$scope之间的桥梁。

#控制器嵌套(作用域包含作用域)
AngularJS在当前作用域中无法找到某个属性时,便会在父级作用域中进行查找。如果AngularJS找不到对应的属性,会顺着父级作用域一直向上寻找,直到抵达$rootScope为止。如果在$rootScope中也找不到,程序会继续运行,但视图无法更新。

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>scope</title>
</head>
<body>
<div ng-app="myApp">
    <div ng-controller="ParentController">
        <div ng-controller="ChildController">
            <button ng-click="sayHello()">sayHello</button>
            {{parent}}
        </div>
    </div>
</div>
<script src="https://cdn.bootcss.com/angular.js/1.2.29/angular.min.js"></script>
<script type="text/javascript">
    var app = angular.module("myApp",[]);
    app.controller("ParentController",function($scope){
        $scope.parent={name:'Tom'};
    });
    app.controller("ChildController",function($scope){
        $scope.sayHello=function(){
            $scope.parent.child='Peter';
        }
    });
</script>
</body>
</html>
```

> 控制器应该尽可能保持短小精悍,而在控制器中不要进行DOM操作和数据操作,设计良好的应用会将复杂的逻辑放到指令和服务中,如同spring的三层结构。

```
angular.module('myApp', []) .controller('MyController', function($scope,UserSrv) {
// 内容可以被指令控制 $scope.onLogin = function(user) {
         UserSrv.runLogin(user);
       };
});
```