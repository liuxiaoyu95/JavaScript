# Express框架之res.render()和res.send()区别

大多数情况下，渲染内容用res.render()，将会根据views中的模板文件进行渲染。如果不想使用views文件夹，想自己设置文件夹名字，那么app.set("views","mb");

```
var express=require('express');
var app=express();
//设计模板引擎   ejs
app.set("views","mb");//设置需要渲染的目录下模板文件
app.set("view engine","ejs");
app.get("/",function(req,res){
    res.render("biaodan",{
        news:['1','2']
    });
    app.listen(3000)
```

如果想写一个快速测试页，当然可以使用res.send()。这个函数将根据内容，自动帮我们设置了Content-Type头部和200状态码。send()只能用一次，和end一样。和end不一样在哪里？能够自动设置MIME类型。

 如果想使用不同的状态码，可以使用(加状态码打点):

```
res.status(404).send('Sorry, we cannot find that!');
```

如果想使用不同的Content-Type，可以：

```
    res.set('Content-Type', 'text/html');
```

实质上res.render用来渲染模板文件,而这个res.send()和res.end(原生)用法基本一致,不过省去了请求头的字符集已经状态码等问题,大大节约我们用来测试!当然也可以自己采用原生的res.end()等,express框架没有自行产生抽象的概念,保留了全部的node原生用法!

转载原文链接:https://cncat.cn/post-244.html