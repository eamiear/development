# 刷新

## Javascript刷新页面的几种方法： 
1. history.go(0) 
2. location.reload() 
3. location=location 
4. location.assign(location) 
5. document.execCommand(‘Refresh’) 
6. window.navigate(location) 
7. location.replace(location) 
8. document.URL=location.href

## 自动刷新页面的方法: 
1. 页面自动刷新：把如下代码加入<head>区域中 
<meta http-equiv=”refresh” content=”20″> 
其中20指每隔20秒刷新一次页面. 

2. 页面自动跳转：把如下代码加入<head>区域中 
<meta http-equiv=”refresh” content=”20;url=http://www.wyxg.com”> 
其中20指隔20秒后跳转到http://www.wyxg.com页面 

3. 页面自动刷新js版 


```html
<script language=”JavaScript”> 
function myrefresh() 
{ 
window.location.reload(); 
} 
setTimeout(‘myrefresh()’,1000); //指定1秒刷新一次 
</script> 
```

