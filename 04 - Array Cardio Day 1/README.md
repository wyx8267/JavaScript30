# 04 - Array Cardio Day 1
## 效果需求
本节主要目的是熟悉Array的几个基本方法，文档给出了初始的inventors数组，基于该数组练习后的结果，可以在浏览器的Console面板中查看。
## 调试技巧
`console.table()`：将结果以表格形式输出。
## 步骤及相关语法
1. 筛选16世纪出生的发明家
    
    使用`filter`，筛选出结果为true的项并组成数组返回。
    ```javascript
    const fifteen = inventors.filter(inventor => {
        if (inventor.year >= 1500 && inventor.year < 1600) {
            return true
        }
    })
    ```
    简化if语句后：
    ```javascript
    const fifteen = inventors.filter(inventor => inventor.year >= 1500 && inventor.year < 1600)
    ```
2. 展示发明家们的姓和名
    
    使用`map()`，特点是会返回与数组中元素个数相同的结果并组成新的数组。
    ```javascript
    const fullNames = inventors.map(inventor => `${inventor.first} ${inventor.last}`)
    ```
3. 按照他们的出生日期从大到小进行排序

    使用`sort()`，需要注意默认会将数组以字符串形式升序排列，所以专门设定一个比较函数：
    ```javascript
    const ordered = inventors.sort((a, b) => a.year > b.year ? 1 : -1)
    ```
4. 计算所有的发明家加起来一共活了多少岁

    使用`reduce()`，该函数可以理解为累加器，接受一个函数作为参数。它会遍历数组的所有项，然后构建一个最终的返回值，这个值就是这个累加器的第一个参数。
    ```javascript
    const totalYears = inventors.reduce((total, inventor) => {
        return total + (inventor.passed - inventor.year)
    }, 0)
    ```
5. 按照他们的岁数来进行排序
    ```javascript
    const oldest = inventors.sort((a, b) => {
        const lastGuy = a.passed - a.year
        const nextGuy = b.passed - b.year
        return lastGuy > nextGuy ? -1 : 1
    })
    ```
6. 筛选出一个网页里含有某个词语的标题

    由于`querySelectorAll()`会返回NodeList，为了进行数组的操作，需要将其转换为数组。有以下两种方式：
    
    ```javascript
    const links = Array.from(category.querySelectorAll('a'))
    const links = [...category.querySelectorAll('a')]
    ```
    `Array.from()` 方法从一个类似数组或可迭代对象创建一个新的，浅拷贝的数组实例。
    
    扩展运算符（spread）三个点`(...)`将一个数组转为用逗号分隔的参数序列。
7. 按照姓氏来对发明家进行排序

    ```javascript
    const alpha = people.sort((lastOne, nextOne) => {
        const [aLast, aFirst] = lastOne.split(', ')
        const [bLast, bFirst] = nextOne.split(', ')
        return aLast > bLast ? 1 : -1
    })
    ```
8. 统计给出数组中各个项的数量
    
    reduce()的参数：`arr.reduce(callback(accumulator, currentValue[, index[, array]])[, initialValue])`

    此处使用`reduce()`时需要统计一个给定数组中各个项的值，在累加器之中，将统计信息存入一个新的对象（此次的initialValue），最后返回统计值。
    ```javascript
    const transportation = data.reduce((obj, item)=>{
        if(!obj[item]){
            obj[item] = 0
        }
        obj[item]++
        return obj
    }, {})
    ```