## My  Front-End experience in programming

------
### Cool Function


```javascript
金额处理：
(2333333333).toLocaleString()
("2333333333333").replace(/\B(?=(\d{3})+(?!\d))/g, ',') //神奇正则

数字交换：
var a = 1, b = 2;
[a, b] = [b, a];

数字字符串转换数字类型
var a = "1"
+a === 1 // true

Set 数组去重(ES6语法)
var arr = [1,2,2,3,4] // 需要去重的数组
var set = new Set(arr) // {1,2,3,4}
var newArr = Array.from(set)

[...new Set([1,2,2,3,4])] // 三点为剩余参数语法，转换为数组

数组填充  Array(6).fill(8)

短路表达式
var a = b && 1 // b is true ,a = 1
var a = b || 1 // b is false,a = 1

数组中取最大，最小值
var numbers = [5, 458 , 120 , -215 , 228 , 400 , 122205, -85411]; 
var maxInNumbers = Math.max.apply(Math, numbers); 
var minInNumbers = Math.min.apply(Math, numbers);










```

### RegExp

-----


```javascript
中文：/^[\u4E00-\u9FA5]+$/

Email ： /\S+@\S+\.\S{3,6}$/

手机号码：/^((13[0-9])|(14[5,7])|(15[0-3,5-9])|(17[0,3,5-8])|(18[0-9])|(147))\d{8}$/

手机号码（简单）/^1\d{10}$/

身份证15~18位：/^[1-9]\d{5}(18|19|([23]\d))\d{2}((0[1-9])|(10|11|12))(([0-2][1-9])|10|20|30|31)\d{3}[0-9Xx]/

固话正则(带分机号验证)：/^0\d{2,3}-\d{5,9}(-\d{1,3})?$/

```

### Code Snippet

----
`URL Param split`
```javascript

function getUrlParam(){
	var url = window.location.href,
	_pa = url.substring(url.indexOf('?') + 1), _arrS = _pa.split('&'), _rs = {};
	for (var i = 0, _len = _arrS.length; i < _len; i++) {
		var pos = _arrS[i].indexOf('=');
		if (pos == -1) {
			continue;
		}
	var name = _arrS[i].substring(0, pos), value =window.decodeURIComponent(_arrS[i].substring(pos + 1));
	_rs[name] = value;
	}
	return _rs;
}

```

`unix时间戳转换`

```javascript
function dateFormat(dat, fmt) { //author: meizz
	
	var o = {
		"M+": dat.getMonth() + 1, //月份
		"d+": dat.getDate(), //日
		"h+": dat.getHours(), //小时
		"m+": dat.getMinutes(), //分
		"s+": dat.getSeconds(), //秒
		"q+": Math.floor((dat.getMonth() + 3) / 3), //季度
		"S": dat.getMilliseconds() //毫秒
	};
	if(/(y+)/.test(fmt))
		fmt = fmt.replace(RegExp.$1, (dat.getFullYear() + "").substr(4 - RegExp.$1.length));
	for(var k in o)
		if(new RegExp("(" + k + ")").test(fmt))
			fmt = fmt.replace(RegExp.$1, (RegExp.$1.length == 1) ? (o[k]) : (("00" + o[k]).substr(("" + o[k]).length)));
	return fmt;
}
//调用方法   dateFormat(new Date(unixtramp * 1000), 'yyyy-MM-dd')；
```