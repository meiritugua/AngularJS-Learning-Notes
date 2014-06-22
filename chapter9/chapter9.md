<h1 style=" -moz-border-radius: 5px; -webkit-border-radius: 5px; -moz-box-shadow: 3px 3px 5px #333; -webkit-box-shadow: 3px 3px 5px #333; box-shadow: 3px 3px 5px #333;  border-radius: 5px; background-color: #69ab01; padding: 4px; color: white; line-height: 1.3em; text-shadow: 2px 2px 2px black; margin: 20px auto; font-size: medium; clear: both;">9. 锚点路由</h1>

<p style="margin: 15px 0;">
准确地说，这应该叫对 <i style=" color: #d75100; font-style: normal; ">hashchange</i> 事件的处理吧。
</p>
<p style="margin: 15px 0;">
就是指 URL 中的锚点部分发生变化时，触发预先定义的业务逻辑。比如现在是 <code style="margin: auto 3px; color: #228b22; font-family: monospace; ">/test#/x</code> ，锚点部分的值为 <code style="margin: auto 3px; color: #228b22; font-family: monospace; ">#</code> 后的 <code style="margin: auto 3px; color: #228b22; font-family: monospace; ">/x</code> ，它就对应了一组处理逻辑。当这部分变化时，比如变成了 <code style="margin: auto 3px; color: #228b22; font-family: monospace; ">/test#/t</code> ，这时页面是不会刷新的，但是它可以触发另外一组处理逻辑，来做一些事，也可以让页面发生变化。
</p>
<p style="margin: 15px 0;">
这种机制对于复杂的单页面来说，无疑是一种强大的业务切分手段。就算不是复杂的单页面应用，在普通页面上善用这种机制，也可以让业务逻辑更容易控制。
</p>
<p style="margin: 15px 0;">
ng 提供了完善的锚点路由功能，虽然目前我觉得相当重要的一个功能还有待完善（后面会说），但目前这功能的几部分内容，已经让我思考了很多种可能性了。
</p>
<p style="margin: 15px 0;">
ng 中的锚点路由功能是由几部分 API 共同完成的一整套方案。这其中包括了路由定义，参数定义，业务处理等。
</p>