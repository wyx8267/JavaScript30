# 13 - Slide in on Scroll

## 实现目标

**文章中的图片在滚入视区时淡入展示，滚出视区外时隐藏**

## 实现步骤

1. 获取页面中的所有图片元素
2. 滚动事件监听
3. 尺寸获取及处理
4. 滚动至指定区域的条件判断

## 功能实现指南

1. 动画涉及CSS属性

  - translateX 元素左右位移
  - opacity 元素不透明程度
  - scale 元素缩放大小

2. 对滚动监听事件添加防抖函数

  ```js
  // 防抖函数
    function debounce(func, wait = 20, immediate = true) {
      var timeout;
      return function() {
        var context = this, args = arguments;
        var later = function() {
          timeout = null;
          if (!immediate) func.apply(context, args);
        };
        var callNow = immediate && !timeout;
        clearTimeout(timeout);
        timeout = setTimeout(later, wait);
        if (callNow) func.apply(context, args);
      };
    }
  ```

  `window.addEventListener('scroll', debounce(checkSlide))`

  添加防抖函数目的：降低监听滚动事件的频率

3. 滚动到指定区域的判断方法

  ```js
  function checkSlide(e){
    sliderImages.forEach(sliderImage => {
      // 图片的一半进入视区
      const slideInAt = (window.scrollY + window.innerHeight) - sliderImage.height / 2;
      // 获取图片底部位置
      const imageBottom = sliderImage.offsetTop + sliderImage.height
      // 判断图片的一半是否已进入指定区域
      const isHalfShown = slideInAt > sliderImage.offsetTop;
      // 判断图片是否在指定区内
      const isNotScrolledPast = window.scrollY < imageBottom;
      // 添加带CSS动画效果的类
      if(isHalfShown && isNotScrolledPast){
        sliderImage.classList.add('active')
      }else{
        sliderImage.classList.remove('active')
      }
    })
  }
  ```
