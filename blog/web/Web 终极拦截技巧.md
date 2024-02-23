---
slug: web-lan-jie
title: Web 终极拦截技巧（全是骚操作）
authors:
  name: 风痕
  title: 十年前的全栈 如今的卑微前端 平时搞点前端工程与音视频
  url: https://github.com/hughfenghen
  image_url: https://avatars.githubusercontent.com/u/3307051?v=4
tags: [web]
---

https://hughfenghen.github.io/posts/2023/12/23/web-spy/

拦截的价值
计算机科学领域的任何问题都可以通过增加一个中间层来解决。 —— Butler Lampson
如果系统的控制权、代码完全被掌控，很容易添加中间层；
现实情况我们往往无法控制系统的所有细节，所以需要使用一些 “非常规”（拦截） 手段来增加中间层。

拦截的方法
#拦截/覆写 浏览器 API
最常见的场景有通过拦截 console 实现错误上报。

```js
const _error = console.error;
console.error = (...args) => {
  _error.apply(console, args);
  console.info('在此处上报错误信息...');
};
// 其它代码打印错误
console.error('error message');
```