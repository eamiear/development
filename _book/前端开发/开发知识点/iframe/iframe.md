# Iframe 基本使用

1. 在iframe中调用本窗口的控件
    ```document.forms["form1"].控件ID.value```
2. 在iframe中调用父窗口的控件
    ```window.parent.forms["form1"].控件ID.value```
3. 在父窗口中调用iframe中的控件
    ```window.frames["iframe窗体ID"].document.forms["form1"].控件ID.value```
4. 在iframe中调用其他iframe的控件
   ``` window.parent.frames["iframe窗体ID"].document.forms["form1"].控件ID.value```
	

注意：

如果系统中存在两个id相同的frame，则可能获取不到iframe对象


5. js获取iframe中的window对象

	

```javascript
var win = $('#ifr')[0].contentWindow;  

window.frames["iframe窗口ID/name"]	//这已经是一个window对象
```


6. iframe 加载完成


# 参考

- [iframes](http://my.oschina.net/u/2409165/blog/551373)
- [iframes-onload-and-documentdomain](https://www.nczonline.net/blog/2009/09/15/iframes-onload-and-documentdomain/)
- [iframes](http://blog.csdn.net/huang100qi/article/details/7852377#reply)

- [jquery-iframe-sizing](http://sonspring.com/journal/jquery-iframe-sizing)
- [auto-resize-iframe-when-content-size-changes](http://www.willmaster.com/library/tutorials/auto-resize-iframe-when-content-size-changes.php)
- [resizing-an-iframe-based-on-content](http://stackoverflow.com/questions/153152/resizing-an-iframe-based-on-content?rq=1)



