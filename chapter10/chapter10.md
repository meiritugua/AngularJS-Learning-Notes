<h1 style=" -moz-border-radius: 5px; -webkit-border-radius: 5px; -moz-box-shadow: 3px 3px 5px #333; -webkit-box-shadow: 3px 3px 5px #333; box-shadow: 3px 3px 5px #333;  border-radius: 5px; background-color: #69ab01; padding: 4px; color: white; line-height: 1.3em; text-shadow: 2px 2px 2px black; margin: 20px auto; font-size: medium; clear: both;">10. 定义模板变量标识标签</h1>

<p style="margin: 15px 0;">
由于下面涉及动态内容，所以我打算起一个后端服务来做。但是我发现我使用的 Tornado 框架的模板系统，与 ng 的模板系统，都是使用 <code style="margin: auto 3px; color: #228b22; font-family: monospace; ">{{ }}</code> 这对符号来定义模板表达式的，这太悲剧了，不过幸好 ng 已经提供了修改方法：
</p>

<div class="highlight" style="background: #103040"><pre style=" white-space: pre-wrap; word-wrap: break-word; border: 1px solid #888; font-size: small; line-height: 1.5em; padding: 5px;; color: #e0eee0; background: #103040;">  <span style="color: #e0eee0">angular</span><span style="color: #7fff00">.</span><span style="color: #e0eee0">bootstrap</span>(<span style="color: #e0eee0">document</span><span style="color: #7fff00">.</span><span style="color: #e0eee0">documentElement</span>,
    [<span style="color: #e0eee0">function</span>(<span style="color: #e0eee0">$interpolateProvider</span>){
      <span style="color: #e0eee0">$interpolateProvider</span><span style="color: #7fff00">.</span><span style="color: #e0eee0">startSymbol</span>(<span style="color: #00e5ee">&#39;[[&#39;</span>);
      <span style="color: #e0eee0">$interpolateProvider</span><span style="color: #7fff00">.</span><span style="color: #e0eee0">endSymbol</span>(<span style="color: #00e5ee">&#39;]]&#39;</span>);
    }]);
</pre></div>


<p style="margin: 15px 0;">
使用 <i style=" color: #d75100; font-style: normal; ">$interpolateProvider</i> 服务即可。
</p>