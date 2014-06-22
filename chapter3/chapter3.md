<h1 style=" -moz-border-radius: 5px; -webkit-border-radius: 5px; -moz-box-shadow: 3px 3px 5px #333; -webkit-box-shadow: 3px 3px 5px #333; box-shadow: 3px 3px 5px #333;  border-radius: 5px; background-color: #69ab01; padding: 4px; color: white; line-height: 1.3em; text-shadow: 2px 2px 2px black; margin: 20px auto; font-size: medium; clear: both;">3. 开始的例子</h1>

<p style="margin: 15px 0;">
我们从一个完整的例子开始认识 ng ：
</p>

<div class="highlight" style="background: #103040"><pre style=" white-space: pre-wrap; word-wrap: break-word; border: 1px solid #888; font-size: small; line-height: 1.5em; padding: 5px;; color: #e0eee0; background: #103040;"><span style="color: gray; padding: 0 5px 0 5px"> 1</span>   <span style="color: #507080">&lt;!DOCTYPE html&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px"> 2</span>   <span style="color: #e0eee0">&lt;html&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px"> 3</span>   <span style="color: #e0eee0">&lt;head&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px"> 4</span>   <span style="color: #e0eee0">&lt;meta</span> <span style="color: #e0eee0">charset=</span><span style="color: #00e5ee">&quot;utf-8&quot;</span> <span style="color: #e0eee0">/&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px"> 5</span>   
<span style="color: gray; padding: 0 5px 0 5px"> 6</span>   <span style="color: #e0eee0">&lt;title&gt;</span>试验<span style="color: #e0eee0">&lt;/title&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px"> 7</span>   
<span style="color: gray; padding: 0 5px 0 5px"> 8</span>   <span style="color: #e0eee0">&lt;script type=</span><span style="color: #00e5ee">&quot;text/javascript&quot;</span> <span style="color: #e0eee0">src=</span><span style="color: #00e5ee">&quot;jquery-1.8.3.js&quot;</span><span style="color: #e0eee0">&gt;&lt;/script&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px"> 9</span>   <span style="color: #e0eee0">&lt;script type=</span><span style="color: #00e5ee">&quot;text/javascript&quot;</span> <span style="color: #e0eee0">src=</span><span style="color: #00e5ee">&quot;angular.js&quot;</span><span style="color: #e0eee0">&gt;&lt;/script&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px">10</span>   
<span style="color: gray; padding: 0 5px 0 5px">11</span>   <span style="color: #e0eee0">&lt;/head&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px">12</span>   <span style="color: #e0eee0">&lt;body&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px">13</span>     <span style="color: #e0eee0">&lt;div</span> <span style="color: #e0eee0">ng-controller=</span><span style="color: #00e5ee">&quot;BoxCtrl&quot;</span><span style="color: #e0eee0">&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px">14</span>       <span style="color: #e0eee0">&lt;div</span> <span style="color: #e0eee0">style=</span><span style="color: #00e5ee">&quot;width: 100px; height: 100px; background-color: red;&quot;</span>
<span style="color: gray; padding: 0 5px 0 5px">15</span>            <span style="color: #e0eee0">ng-click=</span><span style="color: #00e5ee">&quot;click()&quot;</span><span style="color: #e0eee0">&gt;&lt;/div&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px">16</span>       <span style="color: #e0eee0">&lt;p&gt;</span>{{ w }} x {{ h }}<span style="color: #e0eee0">&lt;/p&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px">17</span>       <span style="color: #e0eee0">&lt;p&gt;</span>W: <span style="color: #e0eee0">&lt;input</span> <span style="color: #e0eee0">type=</span><span style="color: #00e5ee">&quot;text&quot;</span> <span style="color: #e0eee0">ng-model=</span><span style="color: #00e5ee">&quot;w&quot;</span> <span style="color: #e0eee0">/&gt;&lt;/p&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px">18</span>       <span style="color: #e0eee0">&lt;p&gt;</span>H: <span style="color: #e0eee0">&lt;input</span> <span style="color: #e0eee0">type=</span><span style="color: #00e5ee">&quot;text&quot;</span> <span style="color: #e0eee0">ng-model=</span><span style="color: #00e5ee">&quot;h&quot;</span> <span style="color: #e0eee0">/&gt;&lt;/p&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px">19</span>     <span style="color: #e0eee0">&lt;/div&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px">20</span>   
<span style="color: gray; padding: 0 5px 0 5px">21</span>   
<span style="color: gray; padding: 0 5px 0 5px">22</span>   <span style="color: #e0eee0">&lt;script type=</span><span style="color: #00e5ee">&quot;text/javascript&quot;</span> <span style="color: #e0eee0">charset=</span><span style="color: #00e5ee">&quot;utf-8&quot;</span><span style="color: #e0eee0">&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px">23</span>   
<span style="color: gray; padding: 0 5px 0 5px">24</span>   
<span style="color: gray; padding: 0 5px 0 5px">25</span>   <span style="color: #bcd2ee">var</span> <span style="color: #e0eee0">BoxCtrl</span> <span style="color: #7fff00">=</span> <span style="color: #bcd2ee">function</span>(<span style="color: #e0eee0">$scope</span>, <span style="color: #e0eee0">$element</span>){
<span style="color: gray; padding: 0 5px 0 5px">26</span>   
<span style="color: gray; padding: 0 5px 0 5px">27</span>     <span style="color: #507080">//$element 就是一个 jQuery 对象</span>
<span style="color: gray; padding: 0 5px 0 5px">28</span>     <span style="color: #bcd2ee">var</span> <span style="color: #e0eee0">e</span> <span style="color: #7fff00">=</span> <span style="color: #e0eee0">$element</span>.<span style="color: #e0eee0">children</span>().<span style="color: #e0eee0">eq</span>(<span style="color: #00ffff">0</span>);
<span style="color: gray; padding: 0 5px 0 5px">29</span>     <span style="color: #e0eee0">$scope</span>.<span style="color: #e0eee0">w</span> <span style="color: #7fff00">=</span> <span style="color: #e0eee0">e</span>.<span style="color: #e0eee0">width</span>();
<span style="color: gray; padding: 0 5px 0 5px">30</span>     <span style="color: #e0eee0">$scope</span>.<span style="color: #e0eee0">h</span> <span style="color: #7fff00">=</span> <span style="color: #e0eee0">e</span>.<span style="color: #e0eee0">height</span>();
<span style="color: gray; padding: 0 5px 0 5px">31</span>   
<span style="color: gray; padding: 0 5px 0 5px">32</span>     <span style="color: #e0eee0">$scope</span>.<span style="color: #e0eee0">click</span> <span style="color: #7fff00">=</span> <span style="color: #bcd2ee">function</span>(){
<span style="color: gray; padding: 0 5px 0 5px">33</span>       <span style="color: #e0eee0">$scope</span>.<span style="color: #e0eee0">w</span> <span style="color: #7fff00">=</span> <span style="color: #e0eee0">parseInt</span>(<span style="color: #e0eee0">$scope</span>.<span style="color: #e0eee0">w</span>) <span style="color: #7fff00">+</span> <span style="color: #00ffff">10</span>;
<span style="color: gray; padding: 0 5px 0 5px">34</span>       <span style="color: #e0eee0">$scope</span>.<span style="color: #e0eee0">h</span> <span style="color: #7fff00">=</span> <span style="color: #e0eee0">parseInt</span>(<span style="color: #e0eee0">$scope</span>.<span style="color: #e0eee0">h</span>) <span style="color: #7fff00">+</span> <span style="color: #00ffff">10</span>;
<span style="color: gray; padding: 0 5px 0 5px">35</span>     }
<span style="color: gray; padding: 0 5px 0 5px">36</span>   
<span style="color: gray; padding: 0 5px 0 5px">37</span>     <span style="color: #e0eee0">$scope</span>.<span style="color: #e0eee0">$watch</span>(<span style="color: #00e5ee">&#39;w&#39;</span>,
<span style="color: gray; padding: 0 5px 0 5px">38</span>       <span style="color: #bcd2ee">function</span>(<span style="color: #e0eee0">to</span>, <span style="color: #e0eee0">from</span>){
<span style="color: gray; padding: 0 5px 0 5px">39</span>         <span style="color: #e0eee0">e</span>.<span style="color: #e0eee0">width</span>(<span style="color: #e0eee0">to</span>);
<span style="color: gray; padding: 0 5px 0 5px">40</span>       }
<span style="color: gray; padding: 0 5px 0 5px">41</span>     );
<span style="color: gray; padding: 0 5px 0 5px">42</span>   
<span style="color: gray; padding: 0 5px 0 5px">43</span>     <span style="color: #e0eee0">$scope</span>.<span style="color: #e0eee0">$watch</span>(<span style="color: #00e5ee">&#39;h&#39;</span>,
<span style="color: gray; padding: 0 5px 0 5px">44</span>       <span style="color: #bcd2ee">function</span>(<span style="color: #e0eee0">to</span>, <span style="color: #e0eee0">from</span>){
<span style="color: gray; padding: 0 5px 0 5px">45</span>         <span style="color: #e0eee0">e</span>.<span style="color: #e0eee0">height</span>(<span style="color: #e0eee0">to</span>);
<span style="color: gray; padding: 0 5px 0 5px">46</span>       }
<span style="color: gray; padding: 0 5px 0 5px">47</span>     );
<span style="color: gray; padding: 0 5px 0 5px">48</span>   }
<span style="color: gray; padding: 0 5px 0 5px">49</span>   
<span style="color: gray; padding: 0 5px 0 5px">50</span>   <span style="color: #e0eee0">angular</span>.<span style="color: #e0eee0">bootstrap</span>(<span style="color: #e0eee0">document</span>.<span style="color: #e0eee0">documentElement</span>);
<span style="color: gray; padding: 0 5px 0 5px">51</span>   <span style="color: #e0eee0">&lt;/script&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px">52</span>   <span style="color: #e0eee0">&lt;/body&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px">53</span>   <span style="color: #e0eee0">&lt;/html&gt;</span>
</pre></div>


<p style="margin: 15px 0;">
从上面的代码中，我们看到在通常的 HTML 代码当中，引入了一些标记，这些就是 ng 的模板机制，它不光完成数据渲染的工作，还实现了数据绑定的功能。
</p>
<p style="margin: 15px 0;">
同时，在 HTML 中的本身的 DOM 层级结构，被 ng 利用起来，直接作为它的内部机制中，上下文结构的判断依据。比如例子中 <i style=" color: #d75100; font-style: normal; ">p</i> 是 <i style=" color: #d75100; font-style: normal; ">div</i> 的子节点，那么 <i style=" color: #d75100; font-style: normal; ">p</i> 中的那些模板标记就是在 <i style=" color: #d75100; font-style: normal; ">div</i> 的 <i style=" color: #d75100; font-style: normal; ">Ctrl</i> 的作用范围之内。
</p>
<p style="margin: 15px 0;">
其它的，也同样写一些 js 代码，里面重要的是作一些数据的操作，事件的绑定定义等。这样，数据的变化就会和页面中的 DOM 表现联系起来。一旦这种联系建立起来，也即完成了我们所说的“双向绑定”。然后，这里说的“事件”，除了那些“点击”等通常的 DOM 事件之外，我们还更关注“数据变化”这个事件。
</p>
<p style="margin: 15px 0;">
最后，可以使用：
</p>

<div class="highlight" style="background: #103040"><pre style=" white-space: pre-wrap; word-wrap: break-word; border: 1px solid #888; font-size: small; line-height: 1.5em; padding: 5px;; color: #e0eee0; background: #103040;">  <span style="color: #e0eee0">angular</span><span style="color: #7fff00">.</span><span style="color: #e0eee0">bootstrap</span>(<span style="color: #e0eee0">document</span><span style="color: #7fff00">.</span><span style="color: #e0eee0">documentElement</span>);
</pre></div>


<p style="margin: 15px 0;">
来把整个页面驱动起来了。（你可以看到一个可被控制大小的红色方块）
</p>
<p style="margin: 15px 0;">
更完整的方法是定义一个 APP ：
</p>

<div class="highlight" style="background: #103040"><pre style=" white-space: pre-wrap; word-wrap: break-word; border: 1px solid #888; font-size: small; line-height: 1.5em; padding: 5px;; color: #e0eee0; background: #103040;"><span style="color: gray; padding: 0 5px 0 5px"> 1</span>   <span style="color: #507080">&lt;!DOCTYPE html&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px"> 2</span>   <span style="color: #e0eee0">&lt;html</span> <span style="color: #e0eee0">ng-app=</span><span style="color: #00e5ee">&quot;MyApp&quot;</span><span style="color: #e0eee0">&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px"> 3</span>   <span style="color: #e0eee0">&lt;head&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px"> 4</span>   <span style="color: #e0eee0">&lt;meta</span> <span style="color: #e0eee0">charset=</span><span style="color: #00e5ee">&quot;utf-8&quot;</span> <span style="color: #e0eee0">/&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px"> 5</span>   
<span style="color: gray; padding: 0 5px 0 5px"> 6</span>   <span style="color: #e0eee0">&lt;title&gt;</span>数据正向绑定<span style="color: #e0eee0">&lt;/title&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px"> 7</span>   
<span style="color: gray; padding: 0 5px 0 5px"> 8</span>   <span style="color: #e0eee0">&lt;script type=</span><span style="color: #00e5ee">&quot;text/javascript&quot;</span> <span style="color: #e0eee0">src=</span><span style="color: #00e5ee">&quot;jquery-1.8.3.js&quot;</span><span style="color: #e0eee0">&gt;&lt;/script&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px"> 9</span>   <span style="color: #e0eee0">&lt;script type=</span><span style="color: #00e5ee">&quot;text/javascript&quot;</span> <span style="color: #e0eee0">src=</span><span style="color: #00e5ee">&quot;angular.js&quot;</span><span style="color: #e0eee0">&gt;&lt;/script&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px">10</span>   
<span style="color: gray; padding: 0 5px 0 5px">11</span>   <span style="color: #e0eee0">&lt;/head&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px">12</span>   <span style="color: #e0eee0">&lt;body&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px">13</span>   
<span style="color: gray; padding: 0 5px 0 5px">14</span>   <span style="color: #e0eee0">&lt;div</span> <span style="color: #e0eee0">ng-controller=</span><span style="color: #00e5ee">&quot;TestCtrl&quot;</span><span style="color: #e0eee0">&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px">15</span>     <span style="color: #e0eee0">&lt;input</span> <span style="color: #e0eee0">type=</span><span style="color: #00e5ee">&quot;text&quot;</span> <span style="color: #e0eee0">value=</span><span style="color: #00e5ee">&quot;&quot;</span> <span style="color: #e0eee0">id=</span><span style="color: #00e5ee">&quot;a&quot;</span> <span style="color: #e0eee0">/&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px">16</span>   <span style="color: #e0eee0">&lt;/div&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px">17</span>   
<span style="color: gray; padding: 0 5px 0 5px">18</span>   
<span style="color: gray; padding: 0 5px 0 5px">19</span>   <span style="color: #e0eee0">&lt;script type=</span><span style="color: #00e5ee">&quot;text/javascript&quot;</span><span style="color: #e0eee0">&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px">20</span>   <span style="color: #bcd2ee">var</span> <span style="color: #e0eee0">TestCtrl</span> <span style="color: #7fff00">=</span> <span style="color: #bcd2ee">function</span>(){
<span style="color: gray; padding: 0 5px 0 5px">21</span>     <span style="color: #e0eee0">console</span>.<span style="color: #e0eee0">log</span>(<span style="color: #00e5ee">&#39;ok&#39;</span>);
<span style="color: gray; padding: 0 5px 0 5px">22</span>   }
<span style="color: gray; padding: 0 5px 0 5px">23</span>   
<span style="color: gray; padding: 0 5px 0 5px">24</span>   <span style="color: #507080">//angular.bootstrap(document.documentElement);</span>
<span style="color: gray; padding: 0 5px 0 5px">25</span>   <span style="color: #e0eee0">angular</span>.<span style="color: #e0eee0">module</span>(<span style="color: #00e5ee">&#39;MyApp&#39;</span>, [], <span style="color: #bcd2ee">function</span>(){<span style="color: #e0eee0">console</span>.<span style="color: #e0eee0">log</span>(<span style="color: #00e5ee">&#39;here&#39;</span>)});
<span style="color: gray; padding: 0 5px 0 5px">26</span>   <span style="color: #e0eee0">&lt;/script&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px">27</span>   
<span style="color: gray; padding: 0 5px 0 5px">28</span>   <span style="color: #e0eee0">&lt;/body&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px">29</span>   <span style="color: #e0eee0">&lt;/html&gt;</span>
</pre></div>


<p style="margin: 15px 0;">
这里说的一个 App 就是 <i style=" color: #d75100; font-style: normal; ">ng</i> 概念中的一个 <i style=" color: #d75100; font-style: normal; ">Module</i> 。对于 <i style=" color: #d75100; font-style: normal; ">Controller</i> 来说， 如果不想使用全局函数，也可以在 app 中定义：
</p>

<div class="highlight" style="background: #103040"><pre style=" white-space: pre-wrap; word-wrap: break-word; border: 1px solid #888; font-size: small; line-height: 1.5em; padding: 5px;; color: #e0eee0; background: #103040;">  <span style="color: #bcd2ee">var</span> <span style="color: #e0eee0">app</span> <span style="color: #7fff00">=</span> <span style="color: #e0eee0">angular</span>.<span style="color: #e0eee0">module</span>(<span style="color: #00e5ee">&#39;MyApp&#39;</span>, [], <span style="color: #bcd2ee">function</span>(){<span style="color: #e0eee0">console</span>.<span style="color: #e0eee0">log</span>(<span style="color: #00e5ee">&#39;here&#39;</span>)});
  <span style="color: #e0eee0">app</span>.<span style="color: #e0eee0">controller</span>(<span style="color: #00e5ee">&#39;TestCtrl&#39;</span>,
    <span style="color: #bcd2ee">function</span>(<span style="color: #e0eee0">$scope</span>){
      <span style="color: #e0eee0">console</span>.<span style="color: #e0eee0">log</span>(<span style="color: #00e5ee">&#39;ok&#39;</span>);
    }
  );
</pre></div>


<p style="margin: 15px 0;">
上面我们使用 <i style=" color: #d75100; font-style: normal; ">ng-app</i> 来指明要使用的 App ，这样的话可以把显式的初始化工作省了。一般完整的过程是：
</p>

<div class="highlight" style="background: #103040"><pre style=" white-space: pre-wrap; word-wrap: break-word; border: 1px solid #888; font-size: small; line-height: 1.5em; padding: 5px;; color: #e0eee0; background: #103040;">  <span style="color: #e0eee0">var</span> <span style="color: #e0eee0">app</span> <span style="color: #7fff00">=</span> <span style="color: #e0eee0">angular</span><span style="color: #7fff00">.</span><span style="color: #e0eee0">module</span>(<span style="color: #00e5ee">&#39;Demo&#39;</span>, <span style="color: #7fff00">[]</span>, <span style="color: #e0eee0">angular</span><span style="color: #7fff00">.</span><span style="color: #e0eee0">noop</span>);
  <span style="color: #e0eee0">angular</span><span style="color: #7fff00">.</span><span style="color: #e0eee0">bootstrap</span>(<span style="color: #e0eee0">document</span>, [<span style="color: #00e5ee">&#39;Demo&#39;</span>]);
</pre></div>


<p style="margin: 15px 0;">
使用 <code style="margin: auto 3px; color: #228b22; font-family: monospace; ">angular.bootstrap</code> 来显示地做初始化工具，参数指明了根节点，装载的模块（可以是多个模块）。
</p>