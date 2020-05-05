---
title: 面试问题总结
date: 2019-10-11 15:29:41
tags: 综合
---

- Axios的特点有哪些
1、在浏览器中发送 XMLHttpRequests 请求；
2、在 node.js 中发送 http请求；
3、基于 Promise 的 HTTP 请求客户端,支持 Promise API；
4、拦截请求和响应；
5、转换请求和响应数据；
6、自动转换 JSON 数据；
7、客户端支持保护安全免受 XSRF 攻击；
<!-- more -->
- vue-router有哪些导航钩子
第一种：是全局导航钩子：router.beforeEach(to,from,next)，作用：跳转前进行判断拦截。
第二种：组件内的钩子
第三种：单独路由独享组件
- 在beforeRouteEnter钩子函数里执行`console.log(this)`，其结果是？
- vue生命周期钩子函数之beforeRouteEnter()和beforeRouteLeave()
```javascript
beforeRouteEnter(to, form, next){
	console.log(this) // undefined
	next(vm =>{
		console.log(vm) // vue实例
	})
}
```

- vue生命周期各个阶段中this的值变化
- vue-router原理
- 深拷贝和浅拷贝
- 解决跨域问题
[vue解决跨域问题](https://segmentfault.com/a/1190000014396546?utm_source=tag-newest)

