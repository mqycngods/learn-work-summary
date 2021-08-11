## ![Alt text](/img/logo.png) 学习or工作总结
### 其他
<details>
<summary>1.获取上个月的当前天是那年那月那日？</summary>
<pre><code>
//针对后端语言的一些特殊函数方法
let kk=new Date().setMonth(new Date().getMonth() - 1)
let ww=new Date(kk)
var y = ww.getFullYear();
var m = ww.getMonth()+1;
var d = ww.getDate();
</code></pre>
</details>
<details>
<summary>2.站外拉起app</summary>
<a href="https://developers.weixin.qq.com/doc/offiaccount/OA_Web_Apps/Wechat_Open_Tag.html">1.微信开放标签</a>
<pre><code>
(1)如何监听跳转成功，取消和失败？
   失败可@error方法
   取消和成功在@launch方法
   原理：异步定时器获取document.visibilityState的状态
   setTimeout(()=>{
        if(document.visibilityState=='hidden'){
            console.log('点击确定，离开页面')
        }
        else if(document.visibilityState=='visible'){
            console.log('点击取消')
        }
    },20)
</code></pre>
<a href="https://www.jianshu.com/p/ab50bdaec65d">2.Universal Link</a>
<pre><code>
原理：当你的应用支持Universal Link(通用链接)，当用户点击一个链接是可以跳转到你的网站并获得无缝重定向到对应的APP，且不需要通过Safari浏览器。如果你的应用不支持的话，则会在Safari中打开该链接。
</code></pre>
</details>
<details>
<summary>3.外部禁止move事件，内部内容显示不全</summary>
<pre><code>
//内部div禁止冒泡，同时禁止穿透
@touchmove.stop="touchMove" id="canmove" @touchstart="touchStart"
touchStart(e) {
    this.firstY = e.targetTouches[0].clientY;
},
touchMove(e) {
    let target = document.getElementById('canmove');
    let offsetHeight = target.offsetHeight,
    scrollHeight = target.scrollHeight;
    let changedTouches = e.changedTouches;
    let scrollTop = target.scrollTop;
    if (changedTouches.length > 0) {
        let touch = changedTouches[0] || {};
        let moveY = touch.clientY;
        if (moveY > this.firstY && scrollTop == 0) {
        // 滑动到弹窗顶部临界条件
        e.preventDefault()
        return false
         } 
        else if (moveY < this.firstY && parseInt(scrollTop + offsetHeight) >= scrollHeight) {
        // 滑动到底部临界条件
        e.preventDefault()
        return false
        }
    }
},

</code></pre>
</details>