我们从一个完整的例子开始认识 ng ：  

```html
  <!DOCTYPE html>  
  <html>  
  <head>  
  <meta charset="utf-8" />  

  <title>试验</title>  

  <script type="text/javascript" src="jquery-1.8.3.js"></script>  
  <script type="text/javascript" src="angular.js"></script>  

  </head>  
  <body>  
    <div ng-controller="BoxCtrl">  
      <div style="width: 100px; height: 100px; background-color: red;"  
	      ng-click="click()"></div>  
	  <p>{{ w }} x {{ h }}</p>  
	  <p>W: <input type="text" ng-model="w" /></p>  
	  <p>H: <input type="text" ng-model="h" /></p>  
    </div>  


  <script type="text/javascript" charset="utf-8">  


  var BoxCtrl = function($scope, $element){  
  

    //$element 就是一个 jQuery 对象  
    var e = $element.children().eq(0);  
    $scope.w = e.width();  
    $scope.h = e.height();   
    
    $scope.click = function(){  
      $scope.w = parseInt($scope.w) + 10;  
      $scope.h = parseInt($scope.h) + 10;  
    }  
    
    $scope.$watch('w',   
      function(to, from){  
        e.width(to);  
      }  
    };   
   
    $scope.$watch('h',  
      function(to, from){  
        e.height(to);  
      }  
    };
  }

  angular.bootstrap(document.documentElement);
  </script>  
  </body>  
  </html>  
```

从上面的代码中，我们看到在通常的 HTML 代码当中，引入了一些标记，这些就是 ng 的模板机制，它不光完成数据渲染的工作，还实现了数据绑定的功能。

同时，在 HTML 中的本身的 DOM 层级结构，被 ng 利用起来，直接作为它的内部机制中，上下文结构的判断依据。比如例子中 `p` 是 `div` 的子节点，那么 `p` 中的那些模板标记
就是在 `div` 的 `Ctrl` 的作用范围之内。

其它的，也同样写一些 js 代码，里面重要的是作一些数据的操作，事件的绑定定义等。这样，数据的变化就会和页面中的 DOM 表现联系起来。一旦这种联系建立起来，
也即完成了我们所说的“双向绑定”。然后，这里说的“事件”，除了那些“点击”等通常的 DOM 事件之外，我们还更关注“数据变化”这个事件。

最后，可以使用：

```html
  angular.bootstrap(document.documentElement);
```  

来把整个页面驱动起来了。（你可以看到一个可被控制大小的红色方块）

更完整的方法是定义一个 APP ：

```html
  <!DOCTYPE html>
  <html ng-app="MyApp">
  <head>  
  <meta charset="utf-8" />  

  <title>数据正向绑定</title>  

  <script type="text/javascript" src="jquery-1.8.3.js"></script>  
  <script type="text/javascript" src="angular.js"></script>  

  </head>  
  <body>  

  <div ng-controller="TestCtrl">  
    <input type="text" value="" id="a" />  
  <div>  

   
  <script type="text/javascript">  
  var TestCtrl = function(){  
    console.log('ok');  
  }

  //angular.bootstrap(document.documentElement);  
  angular.module('MyApp', [], function(){console.log('here')});  
  </script>  

  </body>  
  </html>  
```  

这里说的一个 App 就是 `ng` 概念中的一个 `Module` 。对于 `Controller` 来说， 如果不想使用全局函
局函数，也可以在 app 中定义：

```html
  var app = angular.module('MyApp', [], function(){console.log('here')});  
  app.controller('TestCtrl',  
    function($scope){  
	  console.log('ok');  
	}
  };	  
```   

上面我们使用 `ng-app `来指明要使用的 App ，这样的话可以把显式的初始化工作省了。一般完整的过程是：  

```html
  var app = angular.module('Demo', [], angular.noop); 
  angular.bootstrap(document, ['Demo']);	  
```   

使用 `angular.bootstrap` 来显示地做初始化工具，参数指明了根节点，装载的模块（可以是多个模块）。  
