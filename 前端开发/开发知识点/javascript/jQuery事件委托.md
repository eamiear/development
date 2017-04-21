# 事件委托



```html
<div class="query-list car-detail-list" id="vespertineDetail" style="display: block;">
	<div class="list-count grid text">
		<div class="grid-col text-left">
			<i class="glyphicon glyphicon-chevron-left text-txt" id="back2CarList"></i>
		/div>
		<div class="grid-col text-right">
			<span class="text-txt text-danger">粤A30.0</span>
			<span class="text-txt">跟车点位共<b class="text-muted padding">10</b>个</span>
		</div>
	</div>
</div>
```


```javascript
V.back2CarList = function(){
	$(".car-detail-list").on("click","#back2CarList",function(){
		$(".car-detail-list").hide();
		$(".car-list").show();
	});
}

```



