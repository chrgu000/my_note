- ## CSRF (cross-site request forgery) 跨域请求伪造

	- 也被称为“One Click Attack”或者Session Riding，通常缩写为CSRF或者XSRF，是一种对网站的恶意利用。尽管听起来像跨站脚本（XSS），但它与XSS非常不同，XSS利用站点内的信任用户，而CSRF则通过伪装成受信任用户的请求来利用受信任的网站。与XSS攻击相比，CSRF攻击往往不大流行（因此对其进行防范的资源也相当稀少）和难以防范，所以被认为比XSS更具危险性
	- 攻击通过在授权用户访问的页面中包含链接或者脚本的方式工作。例 如：一个网站用户Bob可能正在浏览聊天论坛，而同时另一个用户Alice也在此论坛中，并且后者刚刚发布了一个具有Bob银行链接的图片消息。设想一下，Alice编写了一个在Bob的银行站点上进行取款的form提交的链接，并将此链接作为图片src。如果Bob的银行在cookie中保存他的授权信息，并且此cookie没有过期，那么当Bob的浏览器尝试装载图片时将提交这个取款form和他的cookie，这样在没经Bob同意的情况下便授权了这次事务。
	- CSRF是一种依赖web浏览器的、被混淆过的代理人攻击（deputy attack）。在上面银行示例中的代理人是Bob的web浏览器，它被混淆后误将Bob的授权直接交给了Alice使用
	- 贴图只是GET的方式，很多时候我们需要伪造POST的请求。一个办法是利用跨站，当然目标站点可能不存在跨站，这个时候我们可以从第三方网站发动攻击。 比如我要攻击一个存在问题的blog，那就先去目标blog留言，留下一个网址，诱其主人点击过来（这个就要看你的忽悠本事咯:p），然后构造个HTML表单提交些数据过去。 多窗口浏览器就帮了一点忙。 多窗口浏览器（firefox、遨游、MyIE……）便捷的同时也带来了一些问题，因为多窗口浏览器新开的窗口是具有当前所有会话的。即我用IE登陆了我的Blog，然后我想看新闻了，又运行一个IE进程，这个时候两个IE窗口的会话是彼此独立的，从看新闻的IE发送请求到Blog不会有我登录的cookie；但是多窗口浏览器永远都只有一个进程，各窗口的会话是通用的，即看新闻的窗口发请求到Blog是会带上我在blog登录的cookie。 想一想，当我们用鼠标在Blog/BBS/WebMail点击别人留下的链接的时候，说不定一场精心准备的CSRF攻击正等着我们

- 防范
	- 对于web站点，将持久化的授权方法（例如cookie或者HTTP授权）切换为瞬时的授权方法（在每个form中提供隐藏field），这将帮助网站防止这些攻击。一种类似的方式是在form中包含秘密信息、用户指定的代号作为cookie之外的验证。 另一个可选的方法是“双提交”cookie。此方法只工作于Ajax请求，但它能够作为无需改变大量form的全局修正方法。如果某个授权的cookie在form post之前正被JavaScript代码读取，那么限制跨域规则将被应用。如果服务器需要在Post请求体或者URL中包含授权cookie的请求，那么这个请求必须来自于受信任的域，因为其它域是不能从信任域读取cookie的。 与通常的信任想法相反，使用Post代替Get方法并不能提供卓有成效的保护。因为JavaScript能使用伪造的POST请求。尽管如此，那些导致对安全产生“副作用”的请求应该总使用Post方式发送。Post方式不会在web服务器和代理服务器日志中留下数据尾巴，然而Get方式却会留下数据尾巴。 尽管CSRF是web应用的基本问题，而不是用户的问题，但用户能够在缺乏安全设计的网站上保护他们的帐户：通过在浏览其它站点前登出站点或者在浏览器会话结束后清理浏览器的cookie。