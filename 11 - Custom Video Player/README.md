# 11 - Custom Video Player

## 实现目标

**为 video 元素添加自定义样式的播放控制面板**
- 可滑动调节音量、播放速度
- 可通过按钮快进、回退
- 可点击视频画面或按钮播放或暂停视频播放
- 可点击或拖动进度条选择视频播放进度

## 实现步骤

1. 获取页面上播放器各部分的元素。
2. 编写播放器播放、快进快退、进度跳转、音量改变、播放速度改变功能。
3. 为各元素添加事件监听。

## 功能实现指南

### 1. 点击播放键或视频切换播放/暂停

video 对象有一个叫`paused`的属性来判断视频是否在播放；另外还提供了两个方法来进行播放和暂停的操作：`.play()`方法可以播放视频，`.pause()`方法暂停播放。同时，根据视频是否为播放状态，切换播放/暂停键的图标。

```javascript
// 切换播放/暂停
function togglePlay() {
  // 1
  if (video.paused) {
    video.play();
  } else {
    video.pause();
  }
  // 2
  const method = video.paused ? 'play' : 'pause';
  video[method]();
  // 3
  video[video.paused ? 'play' : 'pause']();
}
// 对应播放/暂停键图标变化
function updateButton() {
  toggle.textContent = this.paused ? '▶' : '▎▎';
}

video.addEventListener('click', togglePlay);
video.addEventListener('play', updateButton);
video.addEventListener('pause', updateButton);
toggle.addEventListener('click', togglePlay);
```

### 2. 视频前进、后退

从video读取`CurentTime`属性返回一个双精度浮点值，指示以秒为单位的媒体的当前播放位置。设置`data-`属性，在`dataset`中读取。

```html
<button data-skip="-10" class="player__button">« 10s</button>
<button data-skip="25" class="player__button">25s »</button>
```
```javascript
function skip() {
  video.currentTime += parseFloat(this.dataset.skip);
}
```

### 3. 音量与播放速度变化

视频的音量和播放速度这两个滑动条是`range`类型的`input`元素，在元素属性中我们指定了他们各自的最大、最小值和调节的“步值”。

其中需要注意的是，他们分别有一个`volume`和`playbackRate`的`name`属性，我们起这两个名字是因为他们是`video`对象里对应音量和播放速度的两个属性名。这样起名并不是必须的，但可以让我们后面 js 的操作更精简。

通过监听两个`input`元素的`change`事件，我们就可以通过其`value`值改变视频属性了。

```html
<input type="range" name="volume" class="player__slider" min="0" max="1" step="0.05" value="1">
<input type="range" name="playbackRate" class="player__slider" min="0.5" max="2" step="0.1" value="1">
```

```javascript
const ranges = player.querySelectorAll('.player__slider');

function handleRangeUpdate() {
  video[this.name] = this.value;
}

ranges.forEach(range => range.addEventListener('change', handleRangeUpdate));
```

### 4. 进度条操作

进度条显示进度的原理很简单，`progress__filled`这个元素是一个`flex`定位的元素，我们改变其`flex-basis`的百分比值就可以调节它所占父元素的宽度。`flex-basis`值代表`flex`元素在主轴方向上的初始尺寸。

```javascript
function handleProgress() {
  const percent = (video.currentTime / video.duration) * 100;
  progressBar.style.flexBasis = `${percent}%`;
}
video.addEventListener('timeupdate', handleProgress);
```

接着我们需要点击进度条时调整播放进度，那么我们改变进度，或者说宽度就需要得到鼠标点击的位置，这可以通过事件对象的`offsetX`属性来找到，该属性代表鼠标点击位置相对于该元素的水平偏移。得到偏移之后计算出该位置的百分比，那么也就知道了进度的百分比。进度条还要求可以拖动，这个操作我们可以通过设置一个标志来判断当前是否出于拖动状态，然后配合`mousedown`、`mouseup`事件来更新这个标志。

```javascript
function scrub(e) {
  const scrubTime = (e.offsetX / progress.offsetWidth) * video.duration;
  video.currentTime = scrubTime;
}
let mousedown = false;
progress.addEventListener('click', scrub);
progress.addEventListener('mousemove', (e) => mousedown && scrub(e));
progress.addEventListener('mousedown', () => mousedown = true);
progress.addEventListener('mouseup', () => mousedown = false);
```