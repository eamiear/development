# 获取包括元素本身的HTML代码

jQuery中的 .html()方法仅能获取元素内的html代码(不包括自身)。
如果想获取包括自身的HTML代码，可以通过 .prop("outerHTML")获取。

$("#p").prop("outerHTML");