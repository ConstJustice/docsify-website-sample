## 实现 instanceof
```js
function _instanceof(left, right) {
	var proto = left.__proto__
	var prototype = right.prototype
	while(true) {
		if (proto === null) return false
		if (proto === prototype) return ture
		proto = proto.__proto__
	}
}
```

