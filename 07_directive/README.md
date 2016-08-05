# 7.指令
##7.1 自定义HTML元素和属性

###7.1.1 html引导
在HTML中要用内置指令ng-app标记出应用的根节点。这个指令需要以属性的形式来使用,因此可以将它写到任何位置,但是写到`<html>`的开始标签上是最常规的做法.

内置指令是打包在AngularJS内部的指令。所有内置指令的命名空间都使用ng作为前缀。为了防止命名空间冲突,不要在自定义指令前加ng前缀.

###7.1.2 自定义指令
自定义指令myDirective:
```
angular.module('myApp',[]).directive('myDirective', 
function() {
    return {
        restrict: 'E',
        template: '<a href="http://google.com">Click me to go to Google</a>'
    }; 
});
```
使用指令:
```
<my-directive></my-directive>
```
默认情况下,AngularJS将模板生成的HTML代码嵌套在自定义标签<my-directive>内部.

将自定义标签从生成的DOM中完全移除掉, 并只留下由模版生成的链接。将replace设置为true就可以实现这个效果:
```
angular.module('myApp', [])
.directive('myDirective', function() {
    return {
        restrict: 'E',
        replace: true,
        template: '<a href="http://google.com">Click me to go to Google</a>'
    };
});
```

下面指定以元素(E)、属性(A)、类(C)或注释(M)的格式来 调用指令:
```
angular.module('myApp', []).directive('myDirective', 
function() {
    return {
        restrict: 'EAC',
        replace: true,
        template: '<a href="http://google.com">Click me to go to Google</a>'
    }; 
});
```
指令使用:
```
<my-directive></my-directive> 
<div my-directive></div>
<div class="my-directive"></div> 
<!--directive:my-directive-->
```












