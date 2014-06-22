<h1 style=" -moz-border-radius: 5px; -webkit-border-radius: 5px; -moz-box-shadow: 3px 3px 5px #333; -webkit-box-shadow: 3px 3px 5px #333; box-shadow: 3px 3px 5px #333;  border-radius: 5px; background-color: #69ab01; padding: 4px; color: white; line-height: 1.3em; text-shadow: 2px 2px 2px black; margin: 20px auto; font-size: medium; clear: both;">1. 关于AngularJS</h1>

<p style="margin: 15px 0;">
<a href="http://angularjs.org/" style="color: #0184b7; text-decoration: none">AngularJS</a> 是 Google 开源出来的一套 js 工具。下面简称其为 <a href="http://docs.angularjs.org/misc/faq" style="color: #0184b7; text-decoration: none">ng</a> 。这里只说它是“工具”，没说它是完整的“框架”，是因为它并不是定位于去完成一套框架要做的事。更重要的，是它给我们揭示了一种新的应用组织与开发方式。
</p>
<p style="margin: 15px 0;">
ng 最让我称奇的，是它的数据双向绑定。其实想想，我们一直在提数据与表现的分离，但是这里的“双向绑定”从某方面来说，是把数据与表现完全绑定在一起——数据变化，表现也变化。反之，表现变化了，内在的数据也变化。有过开发经验的人能体会到这种机制对于前端应用来说，是很有必要的，能带来维护上的巨大优势。当然，这里的绑定与提倡的分离并不是矛盾的。
</p>
<p style="margin: 15px 0;">
ng 可以和 jQuery 集成工作，事实上，如果没有 jQuery ， ng 自己也做了一个轻量级的 jQuery ，主要实现了元素操作部分的 API 。
</p>
<p style="margin: 15px 0;">
关于 ng 的几点：
</p>

<ul style="line-height: 1.4em; padding: 0px; padding-left: 20px; margin: auto 30px;">
<li>对 IE 方面，它兼容 IE8 及以上的版本。
</li>
<li>与 jQuery 集成工作，它的一些对象与 jQuery 相关对象表现是一致的。
</li>
<li>使用 ng 时不要冒然去改变相关 DOM 的结构。
</li>
</ul>