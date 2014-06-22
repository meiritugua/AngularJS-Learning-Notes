<h1 style=" -moz-border-radius: 5px; -webkit-border-radius: 5px; -moz-box-shadow: 3px 3px 5px #333; -webkit-box-shadow: 3px 3px 5px #333; box-shadow: 3px 3px 5px #333;  border-radius: 5px; background-color: #69ab01; padding: 4px; color: white; line-height: 1.3em; text-shadow: 2px 2px 2px black; margin: 20px auto; font-size: medium; clear: both;">17. 自定义过滤器</h1>

<p style="margin: 15px 0;">
先来回顾一下 ng 中的一些概念：
</p>

<ul style="line-height: 1.4em; padding: 0px; padding-left: 20px; margin: auto 30px;">
<li><i style=" color: #d75100; font-style: normal; ">module</i> ，代码的组织单元，其它东西都是在定义在具体的模块中的。
</li>
<li><i style=" color: #d75100; font-style: normal; ">app</i> ，业务概念，可能会用到多个模块。
</li>
<li><i style=" color: #d75100; font-style: normal; ">service</i> ，仅在数据层面实现特定业务功能的代码封装。
</li>
<li><i style=" color: #d75100; font-style: normal; ">controller</i> ，与 DOM 结构相关联的东西，即是一种业务封装概念，又体现了项目组织的层级结构。
</li>
<li><i style=" color: #d75100; font-style: normal; ">filter</i> ，改变输入数据的一种机制。
</li>
<li><i style=" color: #d75100; font-style: normal; ">directive</i> ，与 DOM 结构相关联的，特定功能的封装形式。
</li>
</ul>

<p style="margin: 15px 0;">
上面的这几个概念基本上就是 ng 的全部。每一部分都可以自由定义，使用时通过各要素的相互配合来实现我们的业务需求。
</p>
<p style="margin: 15px 0;">
我们从最开始一致打交道的东西基本上都是 <i style=" color: #d75100; font-style: normal; ">controller</i> 层面的东西。在前面，也介绍了 <i style=" color: #d75100; font-style: normal; ">module</i> 和 <i style=" color: #d75100; font-style: normal; ">service</i> 的自定义。剩下的会介绍 <i style=" color: #d75100; font-style: normal; ">filter</i> 和 <i style=" color: #d75100; font-style: normal; ">directive</i> 的定义。基本上这几部分的定义形式都是一样的，原理上是通过 <code style="margin: auto 3px; color: #228b22; font-family: monospace; ">provider</code> 来做注入形式的声明，在实际操作过程中，又有很多 shortcut 式的声明方式。
</p>
<p style="margin: 15px 0;">
过滤器的自定义是最简单的，就是一个函数，接受输入，然后返回结果。在考虑过滤器时，我觉得很重要的一点： <b style=" color: red; font-weight: normal; ">无状态</b> 。
</p>
<p style="margin: 15px 0;">
具体来说，过滤器就是一个函数，函数的本质含义就是确定的输入一定得到确定的输出。虽然 <i style=" color: #d75100; font-style: normal; ">filter</i> 是定义在 <i style=" color: #d75100; font-style: normal; ">module</i> 当中的，而且 <i style=" color: #d75100; font-style: normal; ">filter</i> 又是在 <i style=" color: #d75100; font-style: normal; ">controller</i> 的 DOM 范围内使用的，但是，它和具体的 <i style=" color: #d75100; font-style: normal; ">module</i> ， <i style=" color: #d75100; font-style: normal; ">controller</i> ， <i style=" color: #d75100; font-style: normal; ">scope</i> 这些概念都没有关系（虽然在这里你可以使用 js 的闭包机制玩些花样），它仅仅是一个函数，而已。换句话说，它没有任何上下文关联的能力。
</p>
<p style="margin: 15px 0;">
过滤器基本的定义方式：
</p>

<div class="highlight" style="background: #103040"><pre style=" white-space: pre-wrap; word-wrap: break-word; border: 1px solid #888; font-size: small; line-height: 1.5em; padding: 5px;; color: #e0eee0; background: #103040;">  <span style="color: #bcd2ee">var</span> <span style="color: #e0eee0">app</span> <span style="color: #7fff00">=</span> <span style="color: #e0eee0">angular</span>.<span style="color: #e0eee0">module</span>(<span style="color: #00e5ee">&#39;Demo&#39;</span>, [], <span style="color: #e0eee0">angular</span>.<span style="color: #e0eee0">noop</span>);
  <span style="color: #e0eee0">app</span>.<span style="color: #e0eee0">filter</span>(<span style="color: #00e5ee">&#39;map&#39;</span>, <span style="color: #bcd2ee">function</span>(){
    <span style="color: #bcd2ee">var</span> <span style="color: #e0eee0">filter</span> <span style="color: #7fff00">=</span> <span style="color: #bcd2ee">function</span>(<span style="color: #e0eee0">input</span>){
      <span style="color: #90ee90">return</span> <span style="color: #e0eee0">input</span> <span style="color: #7fff00">+</span> <span style="color: #00e5ee">&#39;...&#39;</span>;
    };
    <span style="color: #90ee90">return</span> <span style="color: #e0eee0">filter</span>;
  });
</pre></div>


<p style="margin: 15px 0;">
上面的代码定义了一个叫做 <code style="margin: auto 3px; color: #228b22; font-family: monospace; ">map</code> 的过滤器。使用时：
</p>

<div class="highlight" style="background: #103040"><pre style=" white-space: pre-wrap; word-wrap: break-word; border: 1px solid #888; font-size: small; line-height: 1.5em; padding: 5px;; color: #e0eee0; background: #103040;">  <span style="color: #e0eee0">&lt;p&gt;</span>示例数据: {{ a|map }}<span style="color: #e0eee0">&lt;/p&gt;</span>
</pre></div>


<p style="margin: 15px 0;">
过滤器也可以带参数，多个参数之间使用 <code style="margin: auto 3px; color: #228b22; font-family: monospace; ">:</code> 分割，看一个完整的例子：
</p>

<div class="highlight" style="background: #103040"><pre style=" white-space: pre-wrap; word-wrap: break-word; border: 1px solid #888; font-size: small; line-height: 1.5em; padding: 5px;; color: #e0eee0; background: #103040;"><span style="color: gray; padding: 0 5px 0 5px"> 1</span>   <span style="color: #7fff00">&lt;</span><span style="color: #e0eee0">div</span> <span style="color: #e0eee0">ng</span><span style="color: #7fff00">-</span><span style="color: #e0eee0">controller</span><span style="color: #7fff00">=</span><span style="color: #00e5ee">&quot;TestCtrl&quot;</span><span style="color: #7fff00">&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px"> 2</span>   <span style="color: #7fff00">&lt;</span><span style="color: #e0eee0">p</span><span style="color: #7fff00">&gt;</span>示例数据<span style="color: #7fff00">:</span> {{ <span style="color: #e0eee0">a</span><span style="color: #7fff00">|</span><span style="color: #e0eee0">map</span><span style="color: #7fff00">:</span><span style="color: #e0eee0">map_value</span><span style="color: #7fff00">:</span><span style="color: #00e5ee">&#39;&gt;&gt;&#39;</span><span style="color: #7fff00">:</span><span style="color: #00e5ee">&#39;(no)&#39;</span> }}<span style="color: #7fff00">&lt;</span>/p&gt;
<span style="color: gray; padding: 0 5px 0 5px"> 3</span>   <span style="color: #7fff00">&lt;</span><span style="color: #e0eee0">p</span><span style="color: #7fff00">&gt;</span>示例数据<span style="color: #7fff00">:</span> {{ <span style="color: #e0eee0">b</span><span style="color: #7fff00">|</span><span style="color: #e0eee0">map</span><span style="color: #7fff00">:</span><span style="color: #e0eee0">map_value</span><span style="color: #7fff00">:</span><span style="color: #00e5ee">&#39;&gt;&gt;&#39;</span><span style="color: #7fff00">:</span><span style="color: #00e5ee">&#39;(no)&#39;</span> }}<span style="color: #7fff00">&lt;</span>/p&gt;
<span style="color: gray; padding: 0 5px 0 5px"> 4</span>   <span style="color: #7fff00">&lt;</span>/div&gt;
<span style="color: gray; padding: 0 5px 0 5px"> 5</span>   
<span style="color: gray; padding: 0 5px 0 5px"> 6</span>   
<span style="color: gray; padding: 0 5px 0 5px"> 7</span>   <span style="color: #7fff00">&lt;</span><span style="color: #e0eee0">script</span> <span style="color: #e0eee0">type</span><span style="color: #7fff00">=</span><span style="color: #00e5ee">&quot;text/javascript&quot;</span><span style="color: #7fff00">&gt;</span>
<span style="color: gray; padding: 0 5px 0 5px"> 8</span>   
<span style="color: gray; padding: 0 5px 0 5px"> 9</span>   <span style="color: #bcd2ee">var</span> <span style="color: #e0eee0">app</span> <span style="color: #7fff00">=</span> <span style="color: #e0eee0">angular</span>.<span style="color: #e0eee0">module</span>(<span style="color: #00e5ee">&#39;Demo&#39;</span>, [], <span style="color: #e0eee0">angular</span>.<span style="color: #e0eee0">noop</span>);
<span style="color: gray; padding: 0 5px 0 5px">10</span>   <span style="color: #e0eee0">app</span>.<span style="color: #e0eee0">controller</span>(<span style="color: #00e5ee">&#39;TestCtrl&#39;</span>, <span style="color: #bcd2ee">function</span>(<span style="color: #e0eee0">$scope</span>){
<span style="color: gray; padding: 0 5px 0 5px">11</span>     <span style="color: #e0eee0">$scope</span>.<span style="color: #e0eee0">map_value</span> <span style="color: #7fff00">=</span> {
<span style="color: gray; padding: 0 5px 0 5px">12</span>       <span style="color: #e0eee0">a</span><span style="color: #7fff00">:</span> <span style="color: #00e5ee">&#39;一&#39;</span>,
<span style="color: gray; padding: 0 5px 0 5px">13</span>       <span style="color: #e0eee0">b</span><span style="color: #7fff00">:</span> <span style="color: #00e5ee">&#39;二&#39;</span>,
<span style="color: gray; padding: 0 5px 0 5px">14</span>       <span style="color: #e0eee0">c</span><span style="color: #7fff00">:</span> <span style="color: #00e5ee">&#39;三&#39;</span>
<span style="color: gray; padding: 0 5px 0 5px">15</span>     }
<span style="color: gray; padding: 0 5px 0 5px">16</span>     <span style="color: #e0eee0">$scope</span>.<span style="color: #e0eee0">a</span> <span style="color: #7fff00">=</span> <span style="color: #00e5ee">&#39;a&#39;</span>;
<span style="color: gray; padding: 0 5px 0 5px">17</span>   });
<span style="color: gray; padding: 0 5px 0 5px">18</span>   
<span style="color: gray; padding: 0 5px 0 5px">19</span>   <span style="color: #e0eee0">app</span>.<span style="color: #e0eee0">filter</span>(<span style="color: #00e5ee">&#39;map&#39;</span>, <span style="color: #bcd2ee">function</span>(){
<span style="color: gray; padding: 0 5px 0 5px">20</span>     <span style="color: #bcd2ee">var</span> <span style="color: #e0eee0">filter</span> <span style="color: #7fff00">=</span> <span style="color: #bcd2ee">function</span>(<span style="color: #e0eee0">input</span>, <span style="color: #e0eee0">map_value</span>, <span style="color: #e0eee0">append</span>, <span style="color: #e0eee0">default_value</span>){
<span style="color: gray; padding: 0 5px 0 5px">21</span>       <span style="color: #bcd2ee">var</span> <span style="color: #e0eee0">r</span> <span style="color: #7fff00">=</span> <span style="color: #e0eee0">map_value</span>[<span style="color: #e0eee0">input</span>];
<span style="color: gray; padding: 0 5px 0 5px">22</span>       <span style="color: #90ee90">if</span>(<span style="color: #e0eee0">r</span> <span style="color: #7fff00">===</span> <span style="color: #90ee90">undefined</span>){ <span style="color: #90ee90">return</span> <span style="color: #e0eee0">default_value</span> <span style="color: #7fff00">+</span> <span style="color: #e0eee0">append</span> }
<span style="color: gray; padding: 0 5px 0 5px">23</span>       <span style="color: #90ee90">else</span> { <span style="color: #90ee90">return</span> <span style="color: #e0eee0">r</span> <span style="color: #7fff00">+</span> <span style="color: #e0eee0">append</span> }
<span style="color: gray; padding: 0 5px 0 5px">24</span>     };
<span style="color: gray; padding: 0 5px 0 5px">25</span>     <span style="color: #90ee90">return</span> <span style="color: #e0eee0">filter</span>;
<span style="color: gray; padding: 0 5px 0 5px">26</span>   });
<span style="color: gray; padding: 0 5px 0 5px">27</span>   
<span style="color: gray; padding: 0 5px 0 5px">28</span>   <span style="color: #e0eee0">angular</span>.<span style="color: #e0eee0">bootstrap</span>(<span style="color: #e0eee0">document</span>, [<span style="color: #00e5ee">&#39;Demo&#39;</span>]);
<span style="color: gray; padding: 0 5px 0 5px">29</span>   <span style="color: #7fff00">&lt;</span>/script&gt;
</pre></div>
