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

时间转换(by myself)

var curTime = new Date(),
    year = curTime.getFullYear(),
    mon = curTime.getMonth() + 1,
    day = curTime.getDate(),
    hour = curTime.getHours(),
    min = curTime.getMinutes(),
    sec = curTime.getSeconds(),
    prefix = (...args) => args.map(item => item < 10 ? `0${item}` : item),
    rev = year + prefix(mon, day, hour, min, sec).join("");

console.log(rev);


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

当前数字只能有一个小数点 /^\d?\.?\d+$/

时时替换掉多出来的点(神级操作)
function gaga(obj) { // 值允许输入一个小数点和数字
	obj.value = obj.value.replace(/[^\d.]/g, ""); //先把非数字的都替换掉，除了数字和.
	obj.value = obj.value.replace(/^\./g, ""); //必须保证第一个为数字而不是.
	obj.value = obj.value.replace(/\.{2,}/g, "."); //保证只有出现一个.而没有多个.
	obj.value = obj.value.replace(".", "$#$").replace(/\./g, "").replace("$#$", "."); //保证.只出现一次，而不能出现两次以上
}


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

`browser UA check`

```javascript
    //纯粹判断UA不太准

    !(function() {
        var browser = {
            versions: function() {
                var u = navigator.userAgent,
                    app = navigator.appVersion;
                return { //移动终端浏览器版本信息
                    trident: u.indexOf('Trident') > -1, //IE内核
                    presto: u.indexOf('Presto') > -1, //opera内核
                    webKit: u.indexOf('AppleWebKit') > -1, //苹果、谷歌内核
                    gecko: u.indexOf('Gecko') > -1 && u.indexOf('KHTML') == -1, //火狐内核
                    mobile: !!u.match(/AppleWebKit.*Mobile.*/), //是否为移动终端
                    ios: !!u.match(/\(i[^;]+;( U;)? CPU.+Mac OS X/), //iOS终端
                    android: u.indexOf('Android') > -1 || u.indexOf('Linux') > -1, //android终端或uc浏览器
                    iPhone: u.indexOf('iPhone') > -1, //是否为iPhone或者QQHD浏览器
                    iPad: u.indexOf('iPad') > -1, //是否iPad
                    webApp: u.indexOf('Safari') == -1 //是否web应该程序，没有头部与底部
                };
            }(),
            language: (navigator.browserLanguage || navigator.language).toLowerCase()
        }
        console.log(navigator.versions)
    })();
    

    
    //check browser is mobile?
    var isMobile = function () {
        var isTouch = ('ontouchstart' in window) || window.DocumentTouch && document instanceof DocumentTouch;
        return isTouch || !!navigator.userAgent.match(/AppleWebKit.*Mobile.*!/);
    }()
    console.log(isMobile)
    
    
    
    // check browser is IE?
    function detectIE() {
            var ua = window.navigator.userAgent;
            
            var msie = ua.indexOf('MSIE ');
            if (msie > 0) {
                // IE 10 or older => return version number
                return parseInt(ua.substring(msie + 5, ua.indexOf('.', msie)), 10);
            }

            var trident = ua.indexOf('Trident/');
            if (trident > 0) {
                // IE 11 => return version number
                var rv = ua.indexOf('rv:');
                return parseInt(ua.substring(rv + 3, ua.indexOf('.', rv)), 10);
            }

            var edge = ua.indexOf('Edge/');
            if (edge > 0) {
                // Edge (IE 12+) => return version number
                return parseInt(ua.substring(edge + 5, ua.indexOf('.', edge)), 10);
            }

            // other browser
            return false;
    }
    
```