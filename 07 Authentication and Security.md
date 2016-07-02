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

##Creating the user model
>创建用户模型

First of all, we need to define the model that will be used to represent the users of our
application. 
>首先，我们需要定义将被用来代表的用户的模型提供了应用。 

Laravel already provides you with sensible defaults inside config/auth.
>Laravel已经为您提供了配置/ AUTH内合理的默认值。

php, where you can change the model or table that is used to store your user accounts.
>PHP，在那里你可以更改用于存储用户帐户的模型或表。

It also comes with an existing User model inside app/User.php. 
>它还配备了应用程序/ user.php的内现有用户的模型。

For the purposes of this application, we are going to simplify it slightly, remove certain class variables,
and add new methods so that it can interact with the Cat model as follows:
>为的宗旨这个应用程序，我们要稍微简单点，删除某些类变量，
和添加新的方法，以便它可以如下与猫模型交互：

```php
namespace App;
use Illuminate\Auth\Authenticatable;
use Illuminate\Database\Eloquent\Model;
use Illuminate\Auth\Passwords\CanResetPassword;
use Illuminate\Contracts\Auth\Authenticatable as uthenticableContract;
use Illumunate\Contracts\Auth\CanResetPassword as CanResetPasswordContract;
use App\Cat;
class User extends Model implements AuthenticatableContract,CanResetPasswordContract {
  use Authenticable, CanResetPassword;
  public function cats() {
    return $this->hasMany('App\Cat');
  }
  public function owns(Cat $cat) {
    return $this->id == $cat->user_id;
  }
  public function canEdit(Cat $cat) {
    return $this->is_admin || $this->owns($cat);
  }
}
```

The first thing to note is that this model implements the Authenticable interface.
>首先要注意的一点是，这种模式实现了验证的接口。

Remember that an interface does not give any implementation details. 
>请记住，接口不给出任何实现细节。

It is nothing more than a contract that specifies the names of the methods that a class should
define when it implements the interface. 
>它是什么更重要的是指定的方法的名称一份合同，一个类应当它实现了接口定义。

In this case, the Authenticable interface
mandates that the following methods be implemented:
>在这种情况下，判定真伪的接口任务，以下的方法来实现的：

* getAuthIdentifier
* getAuthPassword
* getRememberToken
* setRememberToken
* getRememberTokenName

If you open the app/User.php file, you might wonder where these methods are.
These methods are actually provided by the Authenticable trait. You can see the
trait being included after the User class's opening brace:

```php
use Authenticable, CanResetPassword;
```
