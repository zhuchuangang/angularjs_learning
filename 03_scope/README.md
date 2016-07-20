#3.作用域

> AngularJS启动并生成视图时,会将根ng-app元素同$rootScope进行绑定。$rootScope是所有$scope对象的最上层。

> $scope对象就是一个普通的JavaScript对象,我们可以在其上随意修改或添加属性。

> $scope对象在AngularJS中充当数据模型,但与传统的数据模型不一样,$scope并不负责处理和操作数据,它只是视图和HTML之间的桥梁,它是视图和控制器之间的胶水。

> 作用域包含了渲染视图时所需的功能和数据,它是所有视图的唯一源头。可以将作用域理解成视图模型(view model)。