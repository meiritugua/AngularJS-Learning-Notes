<h1 style=" -moz-border-radius: 5px; -webkit-border-radius: 5px; -moz-box-shadow: 3px 3px 5px #333; -webkit-box-shadow: 3px 3px 5px #333; box-shadow: 3px 3px 5px #333;  border-radius: 5px; background-color: #69ab01; padding: 4px; color: white; line-height: 1.3em; text-shadow: 2px 2px 2px black; margin: 20px auto; font-size: medium; clear: both;">4. 依赖注入</h1>

<p style="margin: 15px 0;">
<b style=" color: red; font-weight: normal; ">injector</b> ， 我从 ng 的文档中得知这个概念，之后去翻看源码时了解了一下这个机制的工作原理。感觉就是虽然与自己的所想仅差那么一点点，但就是这么一点点，让我感慨想象力之神奇。
</p>
<p style="margin: 15px 0;">
先看我们之前代码中的一处函数定义：
</p>

<div class="highlight" style="background: #103040"><pre style=" white-space: pre-wrap; word-wrap: break-word; border: 1px solid #888; font-size: small; line-height: 1.5em; padding: 5px;; color: #e0eee0; background: #103040;">  <span style="color: #e0eee0">var</span> <span style="color: #e0eee0">BoxCtrl</span> <span style="color: #7fff00">=</span> <span style="color: #e0eee0">function</span>(<span style="color: #e0eee0">$scope</span>, <span style="color: #e0eee0">$element</span>){}
</pre></div>


<p style="margin: 15px 0;">
在这个函数定义中，注意那两个参数： <i style=" color: #d75100; font-style: normal; ">$scope</i> ， <i style=" color: #d75100; font-style: normal; ">$element</i> ，这是两个很有意思的东西。总的来说，它们是参数，这没什么可说的。但又不仅仅是参数——你换个名字代码就不能正常运行了。
</p>
<p style="margin: 15px 0;">
事实上，这两个参数，除了完成“参数”的本身任务之外，还作为一种语法糖完成了“依赖声明”的任务。本来这个函数定义，完整的写法应该像 AMD 声明一样，写成：
</p>

<div class="highlight" style="background: #103040"><pre style=" white-space: pre-wrap; word-wrap: break-word; border: 1px solid #888; font-size: small; line-height: 1.5em; padding: 5px;; color: #e0eee0; background: #103040;">  <span style="color: #e0eee0">var</span> <span style="color: #e0eee0">BoxCtrl</span> <span style="color: #7fff00">=</span> [<span style="color: #00e5ee">&#39;$scope&#39;</span>, <span style="color: #00e5ee">&#39;$element&#39;</span>, <span style="color: #e0eee0">function</span>(<span style="color: #e0eee0">s</span>, <span style="color: #e0eee0">e</span>){}];
</pre></div>


<p style="margin: 15px 0;">
这样就很明显，表示有一个函数，它依赖于两个东西，然后这两个东西会依次作为参数传入。
</p>
<p style="margin: 15px 0;">
简单起见，就写成了一个函数定义原本的样子，然后在定义参数的名字上作文章，来起到依赖声明的作用。
</p>
<p style="margin: 15px 0;">
在处理时，通过函数对象的 <i style=" color: #d75100; font-style: normal; ">toString()</i> 方法可以知道这个函数定义代码的字符串表现形式，然后就知道它的参数是 <i style=" color: #d75100; font-style: normal; ">$scope</i> 和 <i style=" color: #d75100; font-style: normal; ">$element</i> 。通过名字判断出这是两个外部依赖，然后就去获取资源，最后把资源作为参数，调用定义的函数。
</p>
<p style="margin: 15px 0;">
所以，参数的名字是不能随便写的，这里也充分利用了 js 的特点来尽量做到“反省”了。
</p>
<p style="margin: 15px 0;">
在 Python 中受限于函数名的命名规则，写出来不太好看。不过也得利于反省机制，做到这点也很容易：
</p>

<div class="highlight" style="background: #103040"><pre style=" white-space: pre-wrap; word-wrap: break-word; border: 1px solid #888; font-size: small; line-height: 1.5em; padding: 5px;; color: #e0eee0; background: #103040;">  <span style="color: #507080"># -*- coding: utf-8 -*-</span>
  
  <span style="color: #90ee90">def</span> <span style="color: #9bcd9b">f</span>(<span style="color: #e0eee0">Ia</span>, <span style="color: #e0eee0">Ib</span>):
      <span style="color: #90ee90">print</span> <span style="color: #e0eee0">Ia</span>, <span style="color: #e0eee0">Ib</span>
  
  <span style="color: #e0eee0">args</span> <span style="color: #7fff00">=</span> <span style="color: #e0eee0">f</span><span style="color: #7fff00">.</span><span style="color: #e0eee0">func_code</span><span style="color: #7fff00">.</span><span style="color: #e0eee0">co_varnames</span>
  <span style="color: #e0eee0">SRV_MAP</span> <span style="color: #7fff00">=</span> {
      <span style="color: #00e5ee">&#39;Ia&#39;</span>: <span style="color: #00e5ee">&#39;123&#39;</span>,
      <span style="color: #00e5ee">&#39;Ib&#39;</span>: <span style="color: #00e5ee">&#39;456&#39;</span>,
  }
  
  <span style="color: #e0eee0">srv</span> <span style="color: #7fff00">=</span> {}
  <span style="color: #90ee90">for</span> <span style="color: #e0eee0">a</span> <span style="color: #7fff00">in</span> <span style="color: #e0eee0">args</span>:
      <span style="color: #90ee90">if</span> <span style="color: #e0eee0">a</span> <span style="color: #7fff00">in</span> <span style="color: #e0eee0">SRV_MAP</span>:
          <span style="color: #e0eee0">srv</span>[<span style="color: #e0eee0">a</span>] <span style="color: #7fff00">=</span> <span style="color: #e0eee0">SRV_MAP</span>[<span style="color: #e0eee0">a</span>]
  <span style="color: #e0eee0">f</span>(<span style="color: #7fff00">**</span><span style="color: #e0eee0">srv</span>)
</pre></div>