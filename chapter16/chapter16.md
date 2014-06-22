<h1 style=" -moz-border-radius: 5px; -webkit-border-radius: 5px; -moz-box-shadow: 3px 3px 5px #333; -webkit-box-shadow: 3px 3px 5px #333; box-shadow: 3px 3px 5px #333;  border-radius: 5px; background-color: #69ab01; padding: 4px; color: white; line-height: 1.3em; text-shadow: 2px 2px 2px black; margin: 20px auto; font-size: medium; clear: both;">16. AngularJS与其它框架的混用(jQuery, Dojo)</h1>

<p style="margin: 15px 0;">
这个问题似乎很多人都关心，但是事实是，如果了解了 ng 的工作方式，这本来就不是一个问题了。
</p>
<p style="margin: 15px 0;">
在我自己使用 ng 的过程当中，一直是混用 jQuery 的，以前还要加上一个 Dojo 。只要了解每种框架的工作方式，在具体的代码中每个框架都做了什么事，那么整体上控制起来就不会有问题。
</p>
<p style="margin: 15px 0;">
回到 ng 上来看，首先对于 jQuery 来说，最开始说提到过，在 DOM 操作部分， ng 与 jQuery 是兼容的，如果没有 jQuery ， ng 自己也实现了兼容的部分 API 。
</p>
<p style="margin: 15px 0;">
同时，最开始也提到过， ng 的使用最忌讳的一点就是修改 DOM 结构——你应该使用 ng 的模板机制进行数据绑定，以此来控制 DOM 结构，而不是直接操作。换句话来说，在不动 DOM 结构的这个前提之下，你的数据随便怎么改，随便使用哪个框架来控制都是没问题的，到时如有必要使用 <code style="margin: auto 3px; color: #228b22; font-family: monospace; ">$scope.$digest()</code> 来通知 ng 一下即可。
</p>
<p style="margin: 15px 0;">
下面这个例子，我们使用了 jQuery 中的 <i style=" color: #d75100; font-style: normal; ">Deferred</i> ( <code style="margin: auto 3px; color: #228b22; font-family: monospace; ">$.ajax</code> 就是返回一个 <i style=" color: #d75100; font-style: normal; ">Deferred</i> )，还使用了 ng 的 <i style=" color: #d75100; font-style: normal; ">$timeout</i> ，当然是在 ng 的结构之下：
</p>

<div class="highlight" style="background: #103040"><pre style=" white-space: pre-wrap; word-wrap: break-word; border: 1px solid #888; font-size: small; line-height: 1.5em; padding: 5px;; color: #e0eee0; background: #103040;"><span style="color: gray; padding: 0 5px 0 5px"> 1</span>   <span style="color: #507080">&lt;!DOCTYPE html&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px"> 2</span>   <span style="color: #e0eee0">&lt;html</span> <span style="color: #e0eee0">ng-app=</span><span style="color: #00e5ee">&quot;Demo&quot;</span><span style="color: #e0eee0">&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px"> 3</span>   <span style="color: #e0eee0">&lt;head&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px"> 4</span>   <span style="color: #e0eee0">&lt;meta</span> <span style="color: #e0eee0">charset=</span><span style="color: #00e5ee">&quot;utf-8&quot;</span> <span style="color: #e0eee0">/&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px"> 5</span>   <span style="color: #e0eee0">&lt;title&gt;</span>AngularJS<span style="color: #e0eee0">&lt;/title&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px"> 6</span>   <span style="color: #e0eee0">&lt;/head&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px"> 7</span>   <span style="color: #e0eee0">&lt;body&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px"> 8</span>   
<span style="color: gray; padding: 0 5px 0 5px"> 9</span>   <span style="color: #e0eee0">&lt;div</span> <span style="color: #e0eee0">ng-controller=</span><span style="color: #00e5ee">&quot;TestCtrl&quot;</span><span style="color: #e0eee0">&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px">10</span>     <span style="color: #e0eee0">&lt;span</span> <span style="color: #e0eee0">ng-click=</span><span style="color: #00e5ee">&quot;go()&quot;</span><span style="color: #e0eee0">&gt;</span>{{ a }}<span style="color: #e0eee0">&lt;/span&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px">11</span>   <span style="color: #e0eee0">&lt;/div&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px">12</span>   
<span style="color: gray; padding: 0 5px 0 5px">13</span>   <span style="color: #e0eee0">&lt;script type=</span><span style="color: #00e5ee">&quot;text/javascript&quot;</span>
<span style="color: gray; padding: 0 5px 0 5px">14</span>     <span style="color: #e0eee0">src=</span><span style="color: #00e5ee">&quot;http://ajax.googleapis.com/ajax/libs/jquery/1.9.1/jquery.min.js&quot;</span><span style="color: #e0eee0">&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px">15</span>   <span style="color: #e0eee0">&lt;/script&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px">16</span>   <span style="color: #e0eee0">&lt;script type=</span><span style="color: #00e5ee">&quot;text/javascript&quot;</span>
<span style="color: gray; padding: 0 5px 0 5px">17</span>     <span style="color: #e0eee0">src=</span><span style="color: #00e5ee">&quot;http://ajax.googleapis.com/ajax/libs/angularjs/1.0.3/angular.min.js&quot;</span><span style="color: #e0eee0">&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px">18</span>   <span style="color: #e0eee0">&lt;/script&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px">19</span>   
<span style="color: gray; padding: 0 5px 0 5px">20</span>   <span style="color: #e0eee0">&lt;script type=</span><span style="color: #00e5ee">&quot;text/javascript&quot;</span><span style="color: #e0eee0">&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px">21</span>   <span style="color: #bcd2ee">var</span> <span style="color: #e0eee0">app</span> <span style="color: #7fff00">=</span> <span style="color: #e0eee0">angular</span>.<span style="color: #e0eee0">module</span>(<span style="color: #00e5ee">&#39;Demo&#39;</span>, [], <span style="color: #e0eee0">angular</span>.<span style="color: #e0eee0">noop</span>);
<span style="color: gray; padding: 0 5px 0 5px">22</span>   <span style="color: #e0eee0">app</span>.<span style="color: #e0eee0">controller</span>(<span style="color: #00e5ee">&#39;TestCtrl&#39;</span>, <span style="color: #bcd2ee">function</span>(<span style="color: #e0eee0">$scope</span>, <span style="color: #e0eee0">$timeout</span>){
<span style="color: gray; padding: 0 5px 0 5px">23</span>     <span style="color: #e0eee0">$scope</span>.<span style="color: #e0eee0">a</span> <span style="color: #7fff00">=</span> <span style="color: #00e5ee">&#39;点击我开始&#39;</span>;
<span style="color: gray; padding: 0 5px 0 5px">24</span>   
<span style="color: gray; padding: 0 5px 0 5px">25</span>     <span style="color: #bcd2ee">var</span> <span style="color: #e0eee0">defer</span> <span style="color: #7fff00">=</span> <span style="color: #e0eee0">$</span>.<span style="color: #e0eee0">Deferred</span>();
<span style="color: gray; padding: 0 5px 0 5px">26</span>     <span style="color: #bcd2ee">var</span> <span style="color: #e0eee0">f</span> <span style="color: #7fff00">=</span> <span style="color: #bcd2ee">function</span>(){
<span style="color: gray; padding: 0 5px 0 5px">27</span>       <span style="color: #90ee90">if</span>(<span style="color: #e0eee0">$scope</span>.<span style="color: #e0eee0">a</span> <span style="color: #7fff00">==</span> <span style="color: #00e5ee">&#39;&#39;</span>){<span style="color: #e0eee0">$scope</span>.<span style="color: #e0eee0">a</span> <span style="color: #7fff00">=</span> <span style="color: #00e5ee">&#39;已停止&#39;</span>; <span style="color: #90ee90">return</span>}
<span style="color: gray; padding: 0 5px 0 5px">28</span>       <span style="color: #e0eee0">defer</span>.<span style="color: #e0eee0">done</span>(<span style="color: #bcd2ee">function</span>(){
<span style="color: gray; padding: 0 5px 0 5px">29</span>         <span style="color: #e0eee0">$scope</span>.<span style="color: #e0eee0">a</span>.<span style="color: #e0eee0">length</span> <span style="color: #7fff00">&lt;</span> <span style="color: #00ffff">10</span> <span style="color: #7fff00">?</span> <span style="color: #e0eee0">$scope</span>.<span style="color: #e0eee0">a</span> <span style="color: #7fff00">+=</span> <span style="color: #00e5ee">&#39;&gt;&#39;</span> <span style="color: #7fff00">:</span> <span style="color: #e0eee0">$scope</span>.<span style="color: #e0eee0">a</span> <span style="color: #7fff00">=</span> <span style="color: #00e5ee">&#39;&gt;&#39;</span>;
<span style="color: gray; padding: 0 5px 0 5px">30</span>         <span style="color: #e0eee0">$timeout</span>(<span style="color: #e0eee0">f</span>, <span style="color: #00ffff">100</span>);
<span style="color: gray; padding: 0 5px 0 5px">31</span>       });
<span style="color: gray; padding: 0 5px 0 5px">32</span>     }
<span style="color: gray; padding: 0 5px 0 5px">33</span>     <span style="color: #e0eee0">defer</span>.<span style="color: #e0eee0">done</span>(<span style="color: #bcd2ee">function</span>(){<span style="color: #e0eee0">$scope</span>.<span style="color: #e0eee0">a</span> <span style="color: #7fff00">=</span> <span style="color: #00e5ee">&#39;&gt;&#39;</span>; <span style="color: #e0eee0">f</span>()});
<span style="color: gray; padding: 0 5px 0 5px">34</span>   
<span style="color: gray; padding: 0 5px 0 5px">35</span>     <span style="color: #e0eee0">$scope</span>.<span style="color: #e0eee0">go</span> <span style="color: #7fff00">=</span> <span style="color: #bcd2ee">function</span>(){
<span style="color: gray; padding: 0 5px 0 5px">36</span>       <span style="color: #e0eee0">defer</span>.<span style="color: #e0eee0">resolve</span>();
<span style="color: gray; padding: 0 5px 0 5px">37</span>       <span style="color: #e0eee0">$timeout</span>(<span style="color: #bcd2ee">function</span>(){<span style="color: #e0eee0">$scope</span>.<span style="color: #e0eee0">a</span> <span style="color: #7fff00">=</span> <span style="color: #00e5ee">&#39;&#39;</span>}, <span style="color: #00ffff">5000</span>);
<span style="color: gray; padding: 0 5px 0 5px">38</span>     }
<span style="color: gray; padding: 0 5px 0 5px">39</span>   });
<span style="color: gray; padding: 0 5px 0 5px">40</span>   <span style="color: #e0eee0">&lt;/script&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px">41</span>   <span style="color: #e0eee0">&lt;/body&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px">42</span>   <span style="color: #e0eee0">&lt;/html&gt;</span>
</pre></div>


<p style="margin: 15px 0;">
再把 Dojo 加进来看与 DOM 结构相关的例子。之前说过，使用 ng 就最好不要手动修改 DOM 结构，但这里说两点：
</p>

<ol style="line-height: 1.4em; padding: 0px; padding-left: 20px; margin: auto 30px;">
<li>对于整个页面，你可以只在局部使用 ng ，不使用 ng 的地方你可以随意控制 DOM 。
</li>
<li>如果 DOM 结构有变动，你可以在 DOM 结构定下来之后再初始化 ng 。
</li>
</ol>

<p style="margin: 15px 0;">
下面这个例子使用了 <i style=" color: #d75100; font-style: normal; ">AngularJS</i> ， <i style=" color: #d75100; font-style: normal; ">jQuery</i> ， <i style=" color: #d75100; font-style: normal; ">Dojo</i> ：
</p>

<div class="highlight" style="background: #103040"><pre style=" white-space: pre-wrap; word-wrap: break-word; border: 1px solid #888; font-size: small; line-height: 1.5em; padding: 5px;; color: #e0eee0; background: #103040;"><span style="color: gray; padding: 0 5px 0 5px"> 1</span>   <span style="color: #507080">&lt;!DOCTYPE html&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px"> 2</span>   <span style="color: #e0eee0">&lt;html&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px"> 3</span>   <span style="color: #e0eee0">&lt;head&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px"> 4</span>   <span style="color: #e0eee0">&lt;meta</span> <span style="color: #e0eee0">charset=</span><span style="color: #00e5ee">&quot;utf-8&quot;</span> <span style="color: #e0eee0">/&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px"> 5</span>   <span style="color: #e0eee0">&lt;title&gt;</span>AngularJS<span style="color: #e0eee0">&lt;/title&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px"> 6</span>   <span style="color: #e0eee0">&lt;link</span> <span style="color: #e0eee0">rel=</span><span style="color: #00e5ee">&quot;stylesheet&quot;</span>
<span style="color: gray; padding: 0 5px 0 5px"> 7</span>     <span style="color: #e0eee0">href=</span><span style="color: #00e5ee">&quot;http://ajax.googleapis.com/ajax/libs/dojo/1.9.1/dijit/themes/claro/claro.css&quot;</span> <span style="color: #e0eee0">media=</span><span style="color: #00e5ee">&quot;screen&quot;</span> <span style="color: #e0eee0">/&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px"> 8</span>   <span style="color: #e0eee0">&lt;/head&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px"> 9</span>   <span style="color: #e0eee0">&lt;body</span> <span style="color: #e0eee0">class=</span><span style="color: #00e5ee">&quot;claro&quot;</span><span style="color: #e0eee0">&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px">10</span>   
<span style="color: gray; padding: 0 5px 0 5px">11</span>   <span style="color: #e0eee0">&lt;div</span> <span style="color: #e0eee0">ng-controller=</span><span style="color: #00e5ee">&quot;TestCtrl&quot;</span> <span style="color: #e0eee0">id=</span><span style="color: #00e5ee">&quot;test_ctrl&quot;</span><span style="color: #e0eee0">&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px">12</span>   
<span style="color: gray; padding: 0 5px 0 5px">13</span>     <span style="color: #e0eee0">&lt;p</span> <span style="color: #e0eee0">ng-show=</span><span style="color: #00e5ee">&quot;!btn_disable&quot;</span><span style="color: #e0eee0">&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px">14</span>       <span style="color: #e0eee0">&lt;button</span> <span style="color: #e0eee0">ng-click=</span><span style="color: #00e5ee">&quot;change()&quot;</span><span style="color: #e0eee0">&gt;</span>调用dojo修改按钮<span style="color: #e0eee0">&lt;/button&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px">15</span>     <span style="color: #e0eee0">&lt;/p&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px">16</span>   
<span style="color: gray; padding: 0 5px 0 5px">17</span>     <span style="color: #e0eee0">&lt;p</span> <span style="color: #e0eee0">id=</span><span style="color: #00e5ee">&quot;btn_wrapper&quot;</span><span style="color: #e0eee0">&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px">18</span>       <span style="color: #e0eee0">&lt;button</span> <span style="color: #e0eee0">data-dojo-type=</span><span style="color: #00e5ee">&quot;dijit/form/Button&quot;</span> <span style="color: #e0eee0">type=</span><span style="color: #00e5ee">&quot;button&quot;</span><span style="color: #e0eee0">&gt;</span>{{ a }}<span style="color: #e0eee0">&lt;/button&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px">19</span>     <span style="color: #e0eee0">&lt;/p&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px">20</span>   
<span style="color: gray; padding: 0 5px 0 5px">21</span>     <span style="color: #e0eee0">&lt;p&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px">22</span>       <span style="color: #e0eee0">&lt;input</span> <span style="color: #e0eee0">ng-model=</span><span style="color: #00e5ee">&quot;dialog_text&quot;</span> <span style="color: #e0eee0">ng-init=</span><span style="color: #00e5ee">&quot;dialog_text=&#39;对话框内容&#39;&quot;</span> <span style="color: #e0eee0">/&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px">23</span>       <span style="color: #e0eee0">&lt;button</span> <span style="color: #e0eee0">ng-click=</span><span style="color: #00e5ee">&quot;dialog(dialog_text)&quot;</span><span style="color: #e0eee0">&gt;</span>显示对话框<span style="color: #e0eee0">&lt;/button&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px">24</span>     <span style="color: #e0eee0">&lt;/p&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px">25</span>   
<span style="color: gray; padding: 0 5px 0 5px">26</span>     <span style="color: #e0eee0">&lt;p</span> <span style="color: #e0eee0">ng-show=</span><span style="color: #00e5ee">&quot;show_edit_text&quot;</span> <span style="color: #e0eee0">style=</span><span style="color: #00e5ee">&quot;display: none;&quot;</span><span style="color: #e0eee0">&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px">27</span>       <span style="color: #e0eee0">&lt;span&gt;</span>需要编辑的内容:<span style="color: #e0eee0">&lt;/span&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px">28</span>       <span style="color: #e0eee0">&lt;input</span> <span style="color: #e0eee0">ng-model=</span><span style="color: #00e5ee">&quot;text&quot;</span> <span style="color: #e0eee0">/&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px">29</span>     <span style="color: #e0eee0">&lt;/p&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px">30</span>   
<span style="color: gray; padding: 0 5px 0 5px">31</span>     <span style="color: #e0eee0">&lt;div</span> <span style="color: #e0eee0">id=</span><span style="color: #00e5ee">&quot;editor_wrapper&quot;</span><span style="color: #e0eee0">&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px">32</span>       <span style="color: #e0eee0">&lt;div</span> <span style="color: #e0eee0">data-dojo-type=</span><span style="color: #00e5ee">&quot;dijit/Editor&quot;</span> <span style="color: #e0eee0">id=</span><span style="color: #00e5ee">&quot;editor&quot;</span><span style="color: #e0eee0">&gt;&lt;/div&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px">33</span>     <span style="color: #e0eee0">&lt;/div&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px">34</span>   
<span style="color: gray; padding: 0 5px 0 5px">35</span>   <span style="color: #e0eee0">&lt;/div&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px">36</span>   
<span style="color: gray; padding: 0 5px 0 5px">37</span>   
<span style="color: gray; padding: 0 5px 0 5px">38</span>   <span style="color: #e0eee0">&lt;script type=</span><span style="color: #00e5ee">&quot;text/javascript&quot;</span>
<span style="color: gray; padding: 0 5px 0 5px">39</span>     <span style="color: #e0eee0">src=</span><span style="color: #00e5ee">&quot;http://ajax.googleapis.com/ajax/libs/dojo/1.9.1/dojo/dojo.js&quot;</span><span style="color: #e0eee0">&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px">40</span>   <span style="color: #e0eee0">&lt;/script&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px">41</span>   <span style="color: #e0eee0">&lt;script type=</span><span style="color: #00e5ee">&quot;text/javascript&quot;</span>
<span style="color: gray; padding: 0 5px 0 5px">42</span>     <span style="color: #e0eee0">src=</span><span style="color: #00e5ee">&quot;http://ajax.googleapis.com/ajax/libs/jquery/1.9.1/jquery.min.js&quot;</span><span style="color: #e0eee0">&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px">43</span>   <span style="color: #e0eee0">&lt;/script&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px">44</span>   <span style="color: #e0eee0">&lt;script type=</span><span style="color: #00e5ee">&quot;text/javascript&quot;</span>
<span style="color: gray; padding: 0 5px 0 5px">45</span>     <span style="color: #e0eee0">src=</span><span style="color: #00e5ee">&quot;http://ajax.googleapis.com/ajax/libs/angularjs/1.0.3/angular.min.js&quot;</span><span style="color: #e0eee0">&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px">46</span>   <span style="color: #e0eee0">&lt;/script&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px">47</span>   
<span style="color: gray; padding: 0 5px 0 5px">48</span>   <span style="color: #e0eee0">&lt;script type=</span><span style="color: #00e5ee">&quot;text/javascript&quot;</span><span style="color: #e0eee0">&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px">49</span>   
<span style="color: gray; padding: 0 5px 0 5px">50</span>   <span style="color: #e0eee0">require</span>([<span style="color: #00e5ee">&#39;dojo/parser&#39;</span>, <span style="color: #00e5ee">&#39;dijit/Editor&#39;</span>], <span style="color: #bcd2ee">function</span>(<span style="color: #e0eee0">parser</span>){
<span style="color: gray; padding: 0 5px 0 5px">51</span>     <span style="color: #e0eee0">parser</span>.<span style="color: #e0eee0">parse</span>(<span style="color: #e0eee0">$</span>(<span style="color: #00e5ee">&#39;#editor_wrapper&#39;</span>)[<span style="color: #00ffff">0</span>]).<span style="color: #e0eee0">then</span>(<span style="color: #bcd2ee">function</span>(){
<span style="color: gray; padding: 0 5px 0 5px">52</span>       <span style="color: #bcd2ee">var</span> <span style="color: #e0eee0">app</span> <span style="color: #7fff00">=</span> <span style="color: #e0eee0">angular</span>.<span style="color: #e0eee0">module</span>(<span style="color: #00e5ee">&#39;Demo&#39;</span>, [], <span style="color: #e0eee0">angular</span>.<span style="color: #e0eee0">noop</span>);
<span style="color: gray; padding: 0 5px 0 5px">53</span>   
<span style="color: gray; padding: 0 5px 0 5px">54</span>       <span style="color: #e0eee0">app</span>.<span style="color: #e0eee0">controller</span>(<span style="color: #00e5ee">&#39;TestCtrl&#39;</span>, <span style="color: #bcd2ee">function</span>(<span style="color: #e0eee0">$scope</span>, <span style="color: #e0eee0">$timeout</span>){
<span style="color: gray; padding: 0 5px 0 5px">55</span>         <span style="color: #e0eee0">$scope</span>.<span style="color: #e0eee0">a</span> <span style="color: #7fff00">=</span> <span style="color: #00e5ee">&#39;我是ng, 也是dojo&#39;</span>;
<span style="color: gray; padding: 0 5px 0 5px">56</span>         <span style="color: #e0eee0">$scope</span>.<span style="color: #e0eee0">show_edit_text</span> <span style="color: #7fff00">=</span> <span style="color: #90ee90">true</span>;
<span style="color: gray; padding: 0 5px 0 5px">57</span>   
<span style="color: gray; padding: 0 5px 0 5px">58</span>         <span style="color: #e0eee0">$scope</span>.<span style="color: #e0eee0">change</span> <span style="color: #7fff00">=</span> <span style="color: #bcd2ee">function</span>(){
<span style="color: gray; padding: 0 5px 0 5px">59</span>           <span style="color: #e0eee0">$scope</span>.<span style="color: #e0eee0">a</span> <span style="color: #7fff00">=</span> <span style="color: #00e5ee">&#39;DOM结构已经改变(不建议这样做)&#39;</span>;
<span style="color: gray; padding: 0 5px 0 5px">60</span>           <span style="color: #e0eee0">require</span>([<span style="color: #00e5ee">&#39;dojo/parser&#39;</span>, <span style="color: #00e5ee">&#39;dijit/form/Button&#39;</span>, <span style="color: #00e5ee">&#39;dojo/domReady!&#39;</span>],
<span style="color: gray; padding: 0 5px 0 5px">61</span>             <span style="color: #bcd2ee">function</span>(<span style="color: #e0eee0">parser</span>){
<span style="color: gray; padding: 0 5px 0 5px">62</span>               <span style="color: #e0eee0">parser</span>.<span style="color: #e0eee0">parse</span>(<span style="color: #e0eee0">$</span>(<span style="color: #00e5ee">&#39;#btn_wrapper&#39;</span>)[<span style="color: #00ffff">0</span>]);
<span style="color: gray; padding: 0 5px 0 5px">63</span>               <span style="color: #e0eee0">$scope</span>.<span style="color: #e0eee0">btn_disable</span> <span style="color: #7fff00">=</span> <span style="color: #90ee90">true</span>;
<span style="color: gray; padding: 0 5px 0 5px">64</span>             }
<span style="color: gray; padding: 0 5px 0 5px">65</span>           );
<span style="color: gray; padding: 0 5px 0 5px">66</span>         }
<span style="color: gray; padding: 0 5px 0 5px">67</span>   
<span style="color: gray; padding: 0 5px 0 5px">68</span>         <span style="color: #e0eee0">$scope</span>.<span style="color: #e0eee0">dialog</span> <span style="color: #7fff00">=</span> <span style="color: #bcd2ee">function</span>(<span style="color: #e0eee0">text</span>){
<span style="color: gray; padding: 0 5px 0 5px">69</span>           <span style="color: #e0eee0">require</span>([<span style="color: #00e5ee">&quot;dijit/Dialog&quot;</span>, <span style="color: #00e5ee">&quot;dojo/domReady!&quot;</span>], <span style="color: #bcd2ee">function</span>(<span style="color: #e0eee0">Dialog</span>){
<span style="color: gray; padding: 0 5px 0 5px">70</span>             <span style="color: #bcd2ee">var</span> <span style="color: #e0eee0">dialog</span> <span style="color: #7fff00">=</span> <span style="color: #90ee90">new</span> <span style="color: #e0eee0">Dialog</span>({
<span style="color: gray; padding: 0 5px 0 5px">71</span>                 <span style="color: #e0eee0">title</span><span style="color: #7fff00">:</span> <span style="color: #00e5ee">&quot;对话框哦&quot;</span>,
<span style="color: gray; padding: 0 5px 0 5px">72</span>                 <span style="color: #e0eee0">content</span><span style="color: #7fff00">:</span> <span style="color: #e0eee0">text</span>,
<span style="color: gray; padding: 0 5px 0 5px">73</span>                 <span style="color: #e0eee0">style</span><span style="color: #7fff00">:</span> <span style="color: #00e5ee">&quot;width: 300px&quot;</span>
<span style="color: gray; padding: 0 5px 0 5px">74</span>             });
<span style="color: gray; padding: 0 5px 0 5px">75</span>             <span style="color: #e0eee0">dialog</span>.<span style="color: #e0eee0">show</span>();
<span style="color: gray; padding: 0 5px 0 5px">76</span>           });
<span style="color: gray; padding: 0 5px 0 5px">77</span>         }
<span style="color: gray; padding: 0 5px 0 5px">78</span>   
<span style="color: gray; padding: 0 5px 0 5px">79</span>         <span style="color: #e0eee0">require</span>([<span style="color: #00e5ee">&#39;dijit/registry&#39;</span>], <span style="color: #bcd2ee">function</span>(<span style="color: #e0eee0">registry</span>){
<span style="color: gray; padding: 0 5px 0 5px">80</span>           <span style="color: #bcd2ee">var</span> <span style="color: #e0eee0">editor</span> <span style="color: #7fff00">=</span> <span style="color: #e0eee0">registry</span>.<span style="color: #e0eee0">byId</span>(<span style="color: #00e5ee">&#39;editor&#39;</span>);
<span style="color: gray; padding: 0 5px 0 5px">81</span>           <span style="color: #e0eee0">$scope</span>.<span style="color: #e0eee0">$watch</span>(<span style="color: #00e5ee">&#39;text&#39;</span>, <span style="color: #bcd2ee">function</span>(<span style="color: #e0eee0">new_v</span>){
<span style="color: gray; padding: 0 5px 0 5px">82</span>             <span style="color: #e0eee0">editor</span>.<span style="color: #e0eee0">setValue</span>(<span style="color: #e0eee0">new_v</span>);
<span style="color: gray; padding: 0 5px 0 5px">83</span>           });
<span style="color: gray; padding: 0 5px 0 5px">84</span>         });
<span style="color: gray; padding: 0 5px 0 5px">85</span>   
<span style="color: gray; padding: 0 5px 0 5px">86</span>       });
<span style="color: gray; padding: 0 5px 0 5px">87</span>   
<span style="color: gray; padding: 0 5px 0 5px">88</span>       <span style="color: #e0eee0">angular</span>.<span style="color: #e0eee0">bootstrap</span>(<span style="color: #e0eee0">document</span>, [<span style="color: #00e5ee">&#39;Demo&#39;</span>]);
<span style="color: gray; padding: 0 5px 0 5px">89</span>     });
<span style="color: gray; padding: 0 5px 0 5px">90</span>   
<span style="color: gray; padding: 0 5px 0 5px">91</span>   });
<span style="color: gray; padding: 0 5px 0 5px">92</span>   
<span style="color: gray; padding: 0 5px 0 5px">93</span>   <span style="color: #e0eee0">&lt;/script&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px">94</span>   <span style="color: #e0eee0">&lt;/body&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px">95</span>   <span style="color: #e0eee0">&lt;/html&gt;</span>
</pre></div>

