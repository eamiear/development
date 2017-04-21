# 监测刷新操作



```html
<script language="javascript">   
        window.onbeforeunload = function() {   
            var n = window.event.screenX - window.screenLeft;   
            var b = n > document.documentElement.scrollWidth-20;   
            if(b && window.event.clientY < 0 || window.event.altKey){   
                alert("这是一个关闭操作而非刷新");   
                window.event.returnValue = ""; //此处放你想要操作的代码 
            }else{
                alert("这是一个刷新操作而非关闭");   
            }
      }  
</script>
```

