# 返回范围内的随机数
---

javascript只提供了Math.random的随机数生成器，生成随机数的范围是(0,1);
如果需要别的范围的随机数生成，我们可以使用一些数学技巧。

设 Math.random() 为 x:

1. 生成(0,5)随机数
0 < y < 5 
不等式除以5：0 < y / 5 < 1
令：y / 5 = x
所以：y = x * 5
```Math.random() * 5;```

2. 生成(2,5)随机数
2 < y < 5 
不等式减去2：0 < y - 2 < 3
不等式除以5：0 < (y - 2) / 3 < 1
令：(y - 2) / 3 = x
所以：y = x * 3 + 2
```Math.random() * 3 + 2```

3.生成(-3,8)随机数
-3 < y < 8,
不等式加上3: 0 < y + 3 < 11
不等式除以11: 0 < (y + 3) / 11 < 1
令: (y + 3) / 11 = x
所以: y = x * 11 - 3
```
Math.random() * 11 - 3
```

#### 可以推导，对于任意范围 (a,b) 
a < y < b
不等式减去a: 0 < y - a < b - a
不等式除以(b-a): 0 < (y - a)/(b -a) < 1
令: (y - a)/(b - a) = x
所以: y = x(b - a) + a
```
a + Math.random() * (b - a)
```

写成小函数
```
function randIn(a, b) {
	return a + Math.random() * (b - a);
}
```

同理可推导出，任意范围 [a,b] 的**整数**随机数生成器为：
```
function randIn(a, b) {
	return parseInt(a + Math.random() * (b - a + 1));
}
```

---

#### 测试程序
```
function randIn(a, b) {
	return parseInt(a + Math.random() * (b - a + 1));
}

var count_3 = 0;
var count_4 = 0;
var count_5 = 0;
var count_o = 0;

for (var i = 1; i < 1000000; i++) {
	switch(randIn(3,5)) {
		case 3:
			count_3++;
			break;
		case 4:
			count_4++;
			break;
		case 5:
			count_5++;
			break;
		default:
			count_o++;
	}
}

console.log('count_3',count_3);
console.log('count_4',count_4);
console.log('count_5',count_5);
```











