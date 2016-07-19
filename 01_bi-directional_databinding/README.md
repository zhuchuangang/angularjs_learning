#1.hello world程序
```
<!DOCTYPE html>
<html lang="en" ng-app>
<head>
    <meta charset="UTF-8">
    <title>hello world</title>
    <script src="https://cdn.bootcss.com/angular.js/1.5.7/angular.min.js"></script>
</head>
<body>
    Your name:<input ng-model="name" type="text" placeholder="input your name..."/>
    <h1>Hello {{name||'World'}}</h1>
</body>
</html>
```
- `<html>`标记`ng-app`告诉angularjs处理整个html页并引导应用
- 载入angularjs类库`<script src="//cdn.bootcss.com/angular.js/1.5.7/angular.min.js"></script>`,建议把脚本放在 `<body>` 元素的底部, 
提高网页加载速度
- 文本输入指令 `<input ng-model="name" />` 绑定到一个叫name的模型变量。 双大括号标记`{{}}`将name模型变量添加到问候语文本。
所谓的双向绑定就是就是视图数据发生变化模型可以获取到，模型的数据变化视图可以立刻展示。

#2.最佳实践
通常认为,在视图中通过对象的属性而非对象本身来进行引用绑定,是Angular中的最佳实践.
根据最佳实践实现时钟的例子:
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>best practices</title>
    <script src="https://cdn.bootcss.com/angular.js/1.2.29/angular.min.js"></script>
</head>
<body ng-app>
    <div ng-controller="MyController">
        <h1>{{clock.now}}</h1>
    </div>
    <script type="text/javascript" src="js/02_app.js"></script>
</body>
</html>
```
在这个例子中,相比每秒钟都更新$scope.clock,更新$scope.clock.now的值会是更好的选择.
```
// 在app.js中
function MyController($scope) {
         $scope.clock = {
             now: new Date()
         };
         var updateClock = function() {
             $scope.clock.now = new Date()
         };
         setInterval(function() {
             $scope.$apply(updateClock);
}, 1000);
         updateClock();
     };
```
