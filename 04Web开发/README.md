# 为什么`第一方`和`第三方`Cookie不同对待？

- 第一方 Cookie 是你直接访问的域名，它允许网站的拥有者可以搜集分析数据，记住语言设置或者提供很好的用户体验。举例来讲，在你访问社交网站的时候，你并不需要每次都需要重复登陆操作。
- 第三方 Cookie 并不是你正在访问的网站创建的，它通常是由第三方网站创建，用在跨站追踪上或者广告投放。举例来将，在正在浏览的网页上添加一个不可见的元素，浏览器用来向第三方网站发送请求。

```html
<a href="ad.doubleclick.net/some-other-parameters-specific-to-this-ad" target="_blank" rel="noopener"><img src="ad.doubleclick.net/the-extension-to-the-creative"></a>
```

毫无疑问，第一方 Cookie 是互联网用户体验的重要的一部分；但是第三方 Cookie 通常涉及到用户的隐私数据的使用，现在的浏览器一般都可以配置竞争使用第三方 Cookie。