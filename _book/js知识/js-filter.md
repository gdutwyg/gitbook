# filter 妙用

### 去除数组的空字符串删掉
```javascript
var spread = ['A', '', 'B', null, undefined, 'C', '  ']
var filtered = spread.filter((item, idx, arr) => {
  return item && item.trim()
})
console.log('数组中的空字符串删掉', filtered) // => ["A", "B", "C"]

```

### 数组去重

```js
var spread = [12, 5, 8, 8, 130, 44,130]
var filtered = spread.filter((item, idx, arr) => {
  return arr.indexOf(item) === idx;
})
// 筛选符合条件找到的第一个索引值等于当前索引值的数组
console.log('数组去重结果', filtered)

```

```js
var spread = [12, 5, 8, 8, 130, 44,130]
var setFun = [...new Set(spread)]
console.log('数组去重结果', setFun)
```

```js
var arr = [1,3,5];
var arr1 =[1,2,3];
var setFun = [...new Set([...arr, ...arr1])]
console.log('数组去重结果', setFun)
// 获取arr本身有的
setFun.filter((item, i)=> arr.includes(item))
```