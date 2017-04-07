#  Ajax学习笔记
## 1、Ajax概述
`Ajax`的全称是XAsynchronous JavaScript and ML，  
中文定义为：“异步JavaScript和XML”。  
***Web2.0技术的核心***  
有多种技术组合而成，使用Ajax技术不必刷新整个页面，  
只需对当前页面进行局部更新，  可以节省网络带宽，  
提高网页加载速度，从而缩短用户等待时间，改善用户体验。  

## 2、Ajax的工作原理
-  1）JavaScript
-  2）一步数据获取技术XMLHttpRequest
-  3）XML
-  4）DOM
-  5）XHTML和CSS
## 3、常见案例
-    电商网站我们可以动态更新购物车总数 
-    微博社区的点赞按钮
## 4、Http 请求
-    创建XMLHttpRequest 对象
-    我们可以用构造函数的方式，
-    直接new的方式

```javascript
request = new XMLHttpRequest();
```

- 但是这个语句只能针对firefox，safari，
- opera以及chrome等高级浏览器
- 如果我们要针对IE6或者IE6以上的我们就要换一种方式，

```javascript
xmlhttp  = new ActiveXObject("Msxml2.XMLHTTP");
```

- 假如这样创建还不成功，那我们就要换一种方式。

```javascript
xmlhttp  =  new ActiveXObject("Microsoft.XMLHTTP");
```

- 如果这三种方式都不能创建我们的这个对象，
- 那么就说明用户使用的这款浏览器已经过时了，
- 我们可以提示他浏览器不支持Ajax。 
- 好，我们创建的这个对象，
- 首先它必须允许在一个web服务器上的一个网页中，
- 因为它依赖JavaScript，JavaScript必须在网页中才能执行。
- **注意：**
- 我们一定要注意这个网页的编码格式，
- 不然通过异步获取的这些数据有可能是乱码。
- 代码示 例：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <title>Ajax初步入门</title>
</head>
<body>
    <script type="text/javascript">
    function doAjax(the_request){
        var request = null;
        if(window.XMLHttpRequest){
            request = new XMLHttpRequest();
        }else if(window.ActiveXObject){
            request = new ActiveXObject("Microsoft.XMLHTTP");
        }else{
            alert("您的浏览器不支持ajax");
            return false;
        }
    }
    </script>
    <input type="button" onclick="doAjax('ajax-02.txt')" />
    <br /><br />
    <div id="vv"></div>
</body>
</html>
```
- 我们在向服务器发送数据之前，我们有必要了解下多一项的属性。
- 请求服务器有三个比较重要的属性。
- 1）onreadystatechange 属性
- 作用：
- 存储、处理服务器响应的函数
- 2）readyState 属性
-  作用：
- 用来存储服务器响应的状态信息 
-  值：
* 0:表示请求还未初始化，也就是没有发起请求
* 1:表示请求已经提出，在请求发出去之前
* 2:表示请求已经发送，这里通常可以通过响应得到头部信息
* 3:表示服务器正在处理中，但是没有响应完成
* 4:表示服务器已经请求完成，并且使用它
-  这个readyState 值针对的这些状态，
-  我们都要调用onreadystatechange 对应的函数，我们必须在这个函数里，
-  必须添加if语句，才能判断是否完成响应，
-  意味着是否可以获取异步的数据。
r
```javascript
request.onreadtstate = function(){
    //这里要写if语句
    if(request.readyState == 4 ){
    //那说明我们的服务器已经处理完成
    //在里面我们就可以写一些从服务器获取数据的代码，并做相应处理。
}
```

- 3）responseText 属性
-  用来获取服务器返回的数据
- 例如，我们把它打印出来

```javascript
request.onreadtstate = function(){
    //这里要写if语句
    if(request.readyState == 4 ){
    //那说明我们的服务器已经处理完成
    //在里面我们就可以写一些从服务器获取数据的代码，并做相应处理。
alert(request.responseText);
}
```

- 这样我们就把服务器返回的数据，alert出来了
-   这就是我们这个对象的三个属性，但是我们要把请求发送到服务器，
- 那我们就要调用它的两个方法：
-  1、open()
-  它有几个参数
- 1）GET/POST ，表明这个http方法
- 2）URL规定服务器端脚本的URL
- 3）异步处理的标志： 规定应当对请求进行异步的处理
-  2、send() 
- 可以将请求发送到服务器端。
- 我们假设当前这个网页跟我们请求的URL在同一个目录下面，
- **那么我们的代码可以是这样的**

```javascript
request.open("GET","test.txt",true);
request.onreadtstate = function(){
    //这里要写if语句
    if(request.readyState == 4 ){
    //那说明我们的服务器已经处理完成
    //在里面我们就可以写一些从服务器获取数据的代码，并做相应处理。
    alert(request.responseText);
}
request.send(null);
```
