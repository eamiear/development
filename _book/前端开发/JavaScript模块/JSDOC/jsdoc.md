# JSDOC

```JSDOC ```是```JavaScript API``` 文档生成器。通过在```JavaScript```文件中添加注释的方式，生成阅读性高的```HTML```文档。

###安装和使用
```JSDOC```支持```Node.js 0.10``` 及以后的版本，你可以将JSDOC安装在项目的```node_modules```文件夹或者全局环境下。

通过```NPM```安装最新可用版本：

>```npm install jsdoc```

安装最新的开发版本：

>```npm install git+https://github.com/jsdoc3/jsdoc.git```

如果你是本地安装JSDOC，那么JSDOC的命令行工具在```.node_modules/.bin```下，安装下面方式生成一个JavaScript的文档：

>```./node_modules/.bin/jsdoc yourJavaScriptFile.js```


如果你全局安装JSDOC，只需在命令行中执行以下jsdoc命令即可：

>```jsdoc yourJavaScriptFile.js```

默认情况下，生成的文档保存在```out```目录下。可以使用```--destination(-d)```选项来定义其他目录。

执行```jsdoc --help ```查看所有命令行选项清单



```@Link :```  
    [jsdoc github 地址](https://github.com/jsdoc3/jsdoc)  
    [jsdoc 官方文档地址](http://usejsdoc.org/)
