# Requirejs AMD 脚本加载问题

##**Requirejs AMD 问题**

#### 问题说明：
> 由于requirejs 中不支持 
> ` if condtion then dosomething else dootherthing`
> 如：


```javascript
var a;
  if(someCondition) {
       a = require('a1');
  } else {
      a = require('a2');
  }
```


> 如果一个页面内包含tab标签，标签很多或者每块标签的业务繁杂时，首次进入页面时，页面会加载所有的依赖文件，从而造成页面初始化时缓慢
 
#### 解决方案      

```javascript
define(['require','common/base/layout','bootstrap'],function(require,Layout){
    	$(function(){
    		// layout of case management page
    		Layout.initHeight('.tab-content','.nav.nav-tabs');//,21
    		
    		var calendarPanel;
    		var casePanel;
    		var alarmPanel;
    		
            // entry
    		require(['./alarmmgr/AlarmmgrPanel'],function(AlarmmgrPanel){
    			alarmPanel = new AlarmmgrPanel('#alarm');
    		})
    		//calendarPanel = new CalendarPanel('#duty');
    
    		// 切换
            $('a[data-toggle="tab"]').on('shown.bs.tab', function (e) {
                var relatedPaneID = $(e.target).attr('href');
                switch(relatedPaneID){
                	case '#alarm':
    	                if(alarmPanel) return;
    	                alarmPanel = new AlarmmgrPanel(relatedPaneID);
    	                break;
                    case '#case':
                    	if(casePanel) return;
                    	require(['./casemgr/CasemgrPanel'],function(CasemgrPanel){
                    		casePanel = new CasemgrPanel(relatedPaneID);
                    	});
                        break;
                    case '#duty':
                        if(calendarPanel) return;
                        require(['./dutymgr/CalendarPanel'],function(CalendarPanel){
                        	calendarPanel = new CalendarPanel(relatedPaneID);
                    	});
                        break;
                }
            })
    	})
    })
```



