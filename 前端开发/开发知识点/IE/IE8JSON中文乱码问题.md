# IE8JSON中文乱码问题

## JSON 在IE上的情况
1. IE 8以下的浏览器不支持JSON（不包括IE8）
2. IE 8 以上的浏览器支持JSON

## 尿点：
IE8存在的问题：
使用JSON.stringify(data)时，如果data中包含中文字符串，则中文会被编译成Unicode编码。
解决方式：
1. 通过eval()方法解析


```javascript
eval("paramJson = '"+JSON.stringify(data)+"';");
```


2. 使用json2.js的stringify()。由于json2的JSON命名与window的JSON对象命名一致，且浏览器的JSON对象优先使用。估需要将json2.js中的所有JSON改为其他名称。如JSON2，JSON2.stringify();


```html
<!--[if lt IE 9]>
    <script src="http://www.json.org/json2.js"></script>
<![endif]-->
```


## 参考

- [is-json-stringify-supported-by-ie-8](http://stackoverflow.com/questions/3326893/is-json-stringify-supported-by-ie-8)
- [json2](https://github.com/douglascrockford/JSON-js/blob/master/json2.js)