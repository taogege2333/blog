```javascript
/*封装获取水平与垂直滚动的距离，兼容*/
function scroll() {
	if(window.pageYOffset) {
		return {
			"top": window.pageYOffset,
			"left": window.pageXOffset
		}
	} else if(document.compatMode === 'CSS1Compat') {
		return {
			"top": document.documentElement.scrollTop,
			"left": document.documentElement.scrollLeft
		}
	} else {
		return {
			"top": document.body.scrollTop,
			"left": document.body.scrollLeft
		}
	}
}

/*通过id获取dom节点*/
function $(Id) {
	return typeof Id === 'string' ? document.getElementById(Id) : null;
}

/*显示元素*/
function show(obj) {
	obj.style.display = 'block';
}

/*隐藏元素*/
function hide(obj) {
	obj.style.display = 'none';
}

/*封装获取窗口宽高，兼容*/
function client() {
	if(window.innerWidth) {
		return {
			"width": window.innerWidth,
			"height": window.innerHeight
		}
	} else if(document.compatMode === 'CSS1Compat') {
		return {
			"width": document.documentElement.clientWidth,
			"height": document.documentElement.clientHeight
		}
	} else {
		return {
			"width": document.body.clientWidth,
			"height": document.body.clientHeight
		}
	}
}


/*匀速动画*/
//obj:移动元素
// target:目的地
//speedd:速度
function constant(obj, target, speed) {
	//清楚计时器
	clearInterval(obj.timer);
	// 判断方向
	var dir = target > obj.offsetLeft ? speed : -speed;
	obj.timer = setInterval(function () {
		obj.style.left = obj.offsetLeft + dir + 'px';
		//判断剩余距离是否小于步长
		if(Math.abs(target - obj.offsetLeft) < Math.abs(dir)) {
			clearInterval(obj.timer);
			obj.style.left = target + 'px';
		}
	}, 20);
}


/*缓动动画封装*/
//obj:移动元素
// json:{css属性: 目标值}
function buffer(obj, json, fn) {
	//清除定时器
	clearInterval(obj.timer);
	var begin = target = speed = 0;
	obj.timer = setInterval(function () {
		var flag = true;
		for(var key in json) {
			//获取初始值
			if(key === 'opacity') {
				begin = Math.round(parseFloat(getCSSAttrValue(obj, key)) * 100) || 100;
				target = json[key] * 100;
			} else if(key === 'scrollTop') {
				begin = obj.scrollTop;
				target = json[key];
			} else {
				begin = parseInt(getCSSAttrValue(obj, key)) || 0;
				target = json[key];
			}
			//计算步长
			speed = (target - begin)*0.2;
			//判断步长是向上取整还是向下取整
			speed = target > begin ? Math.ceil(speed) : Math.floor(speed);
			//移动
			if(key === 'opacity') {
				//w3c
				obj.style.opacity = (begin + speed) / 100;
				//ie
				obj.style.filter = 'alpha(opacity: '+ (begin + speed) +')'
			} else if(key === 'scrollTop') {
				obj.scrollTop = begin + speed;
			} else {
				obj.style[key] = begin + speed + 'px';
			}

			if(begin !== target) {
				flag = false;
			}
		}
		if(flag) {
			clearInterval(obj.timer);
			if(fn) {
				fn();
			}
		}
	}, 20);

}


/*获取CSS样式值*/
function getCSSAttrValue(obj, attr) {
	if(obj.currentStyle) {
		return obj.currentStyle[attr];
	} else {
		return getComputedStyle(obj, null)[attr];
	}
}


/*封装ajax*/
function Ajax(method, url, success, fail) {
	//创建ajax对象
	if(window.XMLHttpRequest) {
		var ajax = new XMLHttpRequest();
	} else {
		var ajax = new ActiveXObject('Micorosoft XMLHTTP');
	}

	//连接服务器
	ajax.open(method, url, true);
	//发送请求
	ajax.send();
	//接受响应
	ajax.onreadystatechange = function () {
		if(ajax.readyState === 4) {
			if(ajax.status === 200) {
				success(ajax.responseText);
			} else {
				if(fail) {
					fail();
				}
			}
		}
	}

}
```

