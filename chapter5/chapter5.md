<h1 style=" -moz-border-radius: 5px; -webkit-border-radius: 5px; -moz-box-shadow: 3px 3px 5px #333; -webkit-box-shadow: 3px 3px 5px #333; box-shadow: 3px 3px 5px #333;  border-radius: 5px; background-color: #69ab01; padding: 4px; color: white; line-height: 1.3em; text-shadow: 2px 2px 2px black; margin: 20px auto; font-size: medium; clear: both;">5. 作用域</h1>

<p style="margin: 15px 0;">
这里提到的“作用域”的概念，是一个在范围上与 DOM 结构一致，数据上相对于某个 <i style=" color: #d75100; font-style: normal; ">$scope</i> 对象的属性的概念。我们还是从 HTML 代码上来入手：
</p>

<div class="highlight" style="background: #103040"><pre style=" white-space: pre-wrap; word-wrap: break-word; border: 1px solid #888; font-size: small; line-height: 1.5em; padding: 5px;; color: #e0eee0; background: #103040;">  <span style="color: #e0eee0">&lt;div</span> <span style="color: #e0eee0">ng-controller=</span><span style="color: #00e5ee">&quot;BoxCtrl&quot;</span><span style="color: #e0eee0">&gt;</span>
    <span style="color: #e0eee0">&lt;div</span> <span style="color: #e0eee0">style=</span><span style="color: #00e5ee">&quot;width: 100px; height: 100px; background-color: red;&quot;</span>
         <span style="color: #e0eee0">ng-click=</span><span style="color: #00e5ee">&quot;click()&quot;</span><span style="color: #e0eee0">&gt;</span>
    <span style="color: #e0eee0">&lt;/div&gt;</span>
    <span style="color: #e0eee0">&lt;p&gt;</span>{{ w }} x {{ h }}<span style="color: #e0eee0">&lt;/p&gt;</span>
    <span style="color: #e0eee0">&lt;p&gt;</span>W: <span style="color: #e0eee0">&lt;input</span> <span style="color: #e0eee0">type=</span><span style="color: #00e5ee">&quot;text&quot;</span> <span style="color: #e0eee0">ng-model=</span><span style="color: #00e5ee">&quot;w&quot;</span> <span style="color: #e0eee0">/&gt;&lt;/p&gt;</span>
    <span style="color: #e0eee0">&lt;p&gt;</span>H: <span style="color: #e0eee0">&lt;input</span> <span style="color: #e0eee0">type=</span><span style="color: #00e5ee">&quot;text&quot;</span> <span style="color: #e0eee0">ng-model=</span><span style="color: #00e5ee">&quot;h&quot;</span> <span style="color: #e0eee0">/&gt;&lt;/p&gt;</span>
  <span style="color: #e0eee0">&lt;/div&gt;</span>
</pre></div>


<p style="margin: 15px 0;">
上面的代码中，我们给一个 <i style=" color: #d75100; font-style: normal; ">div</i> 元素指定了一个 <i style=" color: #d75100; font-style: normal; ">BoxCtrl</i> ，那么， <i style=" color: #d75100; font-style: normal; ">div</i> 元素之内，就是 <i style=" color: #d75100; font-style: normal; ">BoxCtrl</i> 这个函数运行时， <i style=" color: #d75100; font-style: normal; ">$scope</i> 这个注入资源的控制范围。在代码中我们看到的 <i style=" color: #d75100; font-style: normal; ">click()</i> ， <i style=" color: #d75100; font-style: normal; ">w</i> ， <i style=" color: #d75100; font-style: normal; ">h</i> 这些东西，它们本来的位置对应于 <i style=" color: #d75100; font-style: normal; ">$scope.click</i> ， <i style=" color: #d75100; font-style: normal; ">$scope.w</i> ， <i style=" color: #d75100; font-style: normal; ">$scope.h</i> 。
</p>
<p style="margin: 15px 0;">
我们在后面的 js 代码中，也可以看到我们就是在操作这些变量。依赖于 ng 的数据绑定机制，操作变量的结果直接在页面上表现出来了。
</p>