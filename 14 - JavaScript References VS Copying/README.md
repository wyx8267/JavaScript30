# 14 - JavaScript References VS Copying

1. 拷贝数组

- `arr.slice()`
- `[].concat(arr)`
- `[...arr]`
- `Array.from(arr)`

2. 拷贝对象

- `Object.assign(targetObj, sourceObj)`
- `{...obj}`
- `JSON.parse(JSON.stringify(obj))`