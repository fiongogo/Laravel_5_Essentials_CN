#Authentication and Security
>验证与安全

In this chapter, we will improve the application we built in Chapter 3, Your First
Application, by adding a simple authentication mechanism and addressing any
security issues with the existing code base. 
>在本章中，我们将完善第三章（你的第一个程序)的程序，加入了简单的认证机制和利用现有的
代码库区解决安全问题。


In doing so, you will learn about: 
>通过本章的学习，你将会学习以下内容

* Configuring and using the authentication service 配置和使用的身份验证服务
* Middleware and how to apply it to specific routes 如何在指定的路由中使用中间件
* Data validation and form requests 数据验证和表单请求
* The most common security vulnerabilities in web applications 在Web应用程序中最常见的安全漏洞
* How Laravel can help you write more secure code  Laravel如何帮助你编写更安全的代码

##Authenticating users
>用户验证

Allowing users to register and sign in is an extremely common feature in web applications. 
>允许用户注册并登录是网页应用一种极为常见的功能。

Yet, PHP does not dictate how it should be done, nor does it give you any helpers to implement it. 
>然而，PHP并没有规定它应该怎么做，也不给你任何帮助来实现它。

This has led to the creation of disparate, and sometimes
insecure, methods of authenticating users and restricting access to specific pages. 
>这已经导致建立不同的，有时认证用户和限制访问特定网页不安全，方法。 在

In that respect, Laravel provides you with different tools to make these features more
secure and easier to integrate. 
>这方面，Laravel为您提供不同的工具来使这些功能的更多安全，更容易整合。

It does so with the help of its authentication service
and functionality that we have not covered yet—middleware.
>它与它的身份验证服务的帮助下这样做和功能，我们还没有涵盖尚未中间件。
