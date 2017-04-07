#  Ajax学习笔记
## 1、Ajax概述

- `Ajax`的全称是XAsynchronous JavaScript and ML，   
- 中文定义为：“异步JavaScript和XML”。  
- ***Web2.0技术的核心***  
- 有多种技术组合而成，  使用Ajax技术不必刷新整个页面，  
- 只需对当前页面进行局部更新，  可以节省网络带宽，
- 提高网页加载速度，  从而缩短用户等待时间，       改善用户体验。
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

```
request = new XMLHttpRequest();
```

- 但是这个语句只能针对firefox，safari，
- opera以及chrome等高级浏览器
- 如果我们要针对IE6或者IE6以上的我们就要换一种方式，

```
xmlhttp  = new ActiveXObject("Msxml2.XMLHTTP");
```
- 
- 假如这样创建还不成功，那我们就要换一种方式。

```
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

```
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

