# JSONObject

net.sf.json.JSONObject

1. 调用net.sf.json.JSONObject的put方法时，它不能设置null值
如 o.put('keys',null);
如果要设置空值，这样处理
o.put("keys","null");

2. org.json.JSONObject的处理方式
o.put("keys",JSONObject.NULL);


- [JSONObject](http://www.2cto.com/kf/201411/353461.html)
- [JSONObject](http://www.cnblogs.com/az19870227/archive/2011/09/19/2180993.html)
- [JSONObject](http://blog.csdn.net/yangkai_hudong/article/details/24425729?utm_source=tuicool&utm_medium=referral)