# 10 - Hold Shift to Check Multiple Checkboxes

## 效果需求

选中某个复选框时，其 `<p>` 标签中的文字会显示删除线，按下 Shift 键后能够进行多选操作。

## 实现步骤

1. 获取所有`<input>`元素，并添加事件监听
2. 编写所添加的事件

## 重点逻辑

### 实现按下Shift的多选操作

用一个变量，来标记这个范围。变量初始值为 false，当按下 Shift 键且同时选中了某个元素的时候，遍历所有项，遍历过程中，若遇到 A 或 B，则将标记值取反。同时，将所有标记为 true 的项设置为选中。

```javascript
    let lastChecked
    function handleCheck(e) {
        let inBetween = false
        if (e.shiftKey && this.checked) {
            checkboxes.forEach(checkbox => {
                if (checkbox === this || checkbox === lastChecked) {
                    inBetween = !inBetween
                }
                if (inBetween) {
                    checkbox.checked = true
                }
            })
        }
        lastChecked = this
    }
```
但使用该方法出现了两个问题，待解决：

1. 初次加载页面后，按住Shift点某一选择框，会选中其后所有选项
2. 无法批量操作取消选中
