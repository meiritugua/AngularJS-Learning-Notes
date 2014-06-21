这里提到的“作用域”的概念，是一个在范围上与 DOM 结构一致，数据上相对于某个 $scope 对象的属性的概念。
我们还是从 HTML 代码上来入手：

```html
  <div ng-controller="BoxCtrl">  
    <div style="width: 100px; height: 100px; background-color: red;"  
	    ng-click="click()">  
	</div>  
    <p>{{ w }} x {{ h }}</p>  
    <p>W: <input type="text" ng-model="w" /></p>  
    <p>H: <input type="text" ng-model="h" /></p>  
   </div>  	
```  


上面的代码中，我们给一个 div 元素指定了一个 BoxCtrl ，那么， div 元素之内，
就是 BoxCtrl 这个函数运行时， $scope 这个注入资源的控制范围。
在代码中我们看到的 click() ， w ， h 这些东西，它们本来的位置对应于 $scope.click ， $scope.w ， $scope.h 。

我们在后面的 js 代码中，也可以看到我们就是在操作这些变量。依赖于 ng 的数据绑定机制，操作变量的结果直接在页面上表现出来了。
