title: google voice 申请脚本
tags:
  - google voice
categories:
  - google
date: 2017-10-24 14:18:00
---

###### 选择好号码后在带有continue按钮的界面(下图)，以chrome浏览器为例，选中你需要的号码，按f12键弹出浏览器开发者工具，点击console，在开发者工具console界面，粘贴下面的脚本，回车，你会看到按钮自动点击，接下来等待就可以了。。。

###### 本脚本从别人博客转载的，注意事项什么的，大家自行百度搜索吧。

## JS脚本：
```js
var sleep = delay => new Promise(resolve => setTimeout(resolve, delay));

var composeClick = function x(btn) {
  var rect = btn.getBoundingClientRect();
  var x = rect.left + rect.width * Math.random();
  var y = rect.top + rect.height * Math.random();
  const mousedown = new MouseEvent("mousedown", {
    screenX: x + window.screen.availLeft,
    screenY: y + window.screen.availTop,
    clientX: x,
    clientY: y,
  });
  const click = new MouseEvent("click", {
    screenX: x + window.screen.availLeft,
    screenY: y + window.screen.availTop,
    clientX: x,
    clientY: y,
  });
  const mouseup = new MouseEvent("mouseup", {
    screenX: x + window.screen.availLeft,
    screenY: y + window.screen.availTop,
    clientX: x,
    clientY: y,
  });
  btn.dispatchEvent(mousedown);
  return sleep(150 + Math.random() * 30)
    .then(() => {
      btn.dispatchEvent(click);
      return sleep(30 + Math.random() * 30);
    }).then(() => {
      btn.dispatchEvent(mouseup);
    });
}

function task() {
  var btn = document.querySelector(".continueButton");
  if (!btn) {
    alert("Finish");
    return;
  }
  composeClick(btn)
    .then(() => {
      // 在此调整点击时间间隔
      return sleep(50 + Math.random() * 600);
    })
    .then(() => {
      task();
    });
}
task();

```



## 注意事项

##### 1、 新注册的Google账号，然后申请GV, 千万不要跳IP登录。否则被封的几率非常大。

##### 2、有人说环聊安卓无法接收来电？请仔细研究环聊设置中是否开启了 【来电】开关。记住全程挂美国代理。

##### 3、Google Voice有回收政策，而不回收的前提就是半年内使用Google Voice号码发短信或者打电话，这点还是很容易做到的。