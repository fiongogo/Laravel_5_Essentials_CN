#Filtering Requests with Middleware  
>通过中间件中过滤请求

In this chapter, middleware will be discussed in detail and examples from the 
accommodation software will be provided. 
>在这一章中，将详细讨论中间件，并且给予相应的例子。

Middleware is a great mechanism to help separate a software application into 
separate layers. 

To illustrate this principle,middleware provides layers of protection around the 
innermost part of the application, which could be thought of as the kernel.

In Laravel 4, middleware was known as filters. 

These filters were used in routing to perform actions that came before the controller 
like authentication, where the user would be filtered based on certain criteria. 
Also, the filters could comeafter the controller.

In Laravel 5, the concept of middleware, which was already present but not prominent 
in Laravel 4, is now brought into the foreground into the actual request
workflow and can be used in various ways. Think of it as a Russian doll, where each
doll represents a layer in the application—having the correct credentials will allow
us to enter deeper into the application.
