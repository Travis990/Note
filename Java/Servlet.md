## 一、Servlet方法

**Servlet需要提供对应的`doGet()`/`doPost()`方法**

### doGet()

- `form`默认的提交方式
- 指定超链接访问某个地址
- 在地址栏里直接输入某个地址
- `AJAX`指定使用`get`方式

### doPost()

- `form`上指定`method="post"`；
- `AJAX`指定使用`post`方式；

### service()

```java
service(HttpServletRequest, HttpServletResponse);
```

- 在执行`doGet()`和`doPos()`之前都会先执行`service()`；
- `service()`方法进行判断，调用哪一种方法；

## 传递中文参数

**HTML文件中设置utf-8编码**

```html
<meta charset="utf-8" />
```

**将读到的参数进行解码和编码**

```java
byte[] bytes=  name.getBytes("ISO-8859-1");
name = new String(bytes,"UTF-8");
```

**或者直接将请求统一成utf-8编码**

```java
request.setCharacterEncoding("utf-8"); 
```

**同理，返回中文也需要把response统一成utf-8编码**

```java
response.setContentType("text/html; charset=UTF-8");
```

## 二、生命周期

**实例化 --> 初始化 --> 提供服务 --> 销毁 --> 被回收**

#### 实例化

- 当浏览器输入一个路径，其对应的servlet被调用的时候，该servlet就会被实例化；
- 一个servlet只会被实例化一次；

#### 初始化

- 继承自`HttpServlet`，也继承了`init()`方法；
- `init()`方法是一个实例方法，会在构造函数执行后再执行；
- `init()`同样只会执行一次；

#### 提供服务

- 执行`service()`方法，通过浏览器传递的信息进行判断，执行`doGet()/doPost()`；

#### 销毁

- 执行`destroy()`方法；
- web应用关闭/重启时执行；

#### 被回收

servlet被销毁后，下次GC就会被回收了

## 三、页面跳转

#### 服务端跳转

- 服务端验证密码，访问对应的html文件，把文件内容传给浏览器；
- 浏览器url不跳转，页面内容改变

```java
request.getRequestDispatcher("success.html").forward(request, response);
```

#### 客户端跳转

- 服务端验证密码，发送跳转指令给浏览器，浏览器接受指令，申请对应的html页面，服务端把申请的html文件内容传给浏览器；
- 浏览器url改变；

```java
response.sendRedirect("fail.html");
```