# 今天总结

一、模拟call的实现

思路分三步：
 - 将函数挂载到上下文
 - 执行函数
 - 删除函数

```js
// 第一步
foo.fn = bar
// 第二步
foo.fn()
// 第三步
delete foo.fn
```

具体实现如下：
```js
Function.prototype.myCall = function(context) {
	var context || window // 当context不传时this为window
	context.fn = this // 方法名无所谓，反正调用结束即刻删除
	var args = []
	for (var i = 1; i < arguments.length; i++) {
		args.push('arguments[' + i + ']');
	}
	var result = eval('context.fn(' + args.toString() +')'') // 关键一步，巧用eval解决参数传递
	delete context.fn // 删除方法
	return result // 返回调用结果
}
```

二、模拟apply实现
思路与call类似，判断第二个参数即可
具体实现如下：
```js
Function.prototype.myApply = function(context, arr) {
	var context || window
	context.fn = this
	
	var result
	if (!arr) {
		result = context.fn()
	} else {
		var args = []
		for (var i = 1; i < arguments.length; i++) {
			args.push('arguments[' + i + ']');
		}
		result = eval('context.fn(' + args.toString() +')'')
	}
	delete context.fn // 删除方法
	return result // 返回调用结果
}
```

三、模拟bind实现
bind的实现需要考虑
1、bind（context, args[1], args[2]）参数传输
2、如果调用bind的函数为构造函数，则context会被忽略

```js
Function.prototype.myBind = function (context) {

    if (typeof this !== "function") {
      throw new Error("Function.prototype.bind - what is trying to be bound is not callable");
    }

    var self = this;
    var args = Array.prototype.slice.call(arguments, 1);

    var fNOP = function () {};

    var fBound = function () {
        var bindArgs = Array.prototype.slice.call(arguments);
        return self.apply(this instanceof fNOP ? this : context, args.concat(bindArgs));
    }

    fNOP.prototype = this.prototype; // 这两步容我细品
    fBound.prototype = new fNOP();
    return fBound;
}
```