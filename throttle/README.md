## 节流&防抖

在前端开发中有一部分用户会频繁触发事件执行，对于DOM操作、资源加载等耗费性能的处理，很可能导致页面卡顿，甚至浏览器崩溃。函数节流（throttle）和函数防抖（debounce）就是为了解决类似需求应运而生

### 节流

函数节流就是预定一个函数只有在大于等于执行周期时才执行，周期内调用不执行。好像水滴攒到一定量才会溢出一样

### 场景

- 窗口的调整（resize）
- 页面滚动（scroll）
- 抢购疯狂点击（mousedwon）

```
<div id="show">0</div>
<button id="btn"></button>
<script>
	var oDiv = document.getElementById('show');
    var oBtn = document.getElementById('btn');
    
    function throttle(handle, wait) {
        var lastTime = 0;
        return function (e) {
            // arguments [event]
            var nowTime = new Date().getTime();
            if (nowTime - lastTime > wait) {
                handle.apply(this, arguments)
                lastTime = nowTime;
            }
        }
    }
    
    function buy(e) {
        console.log(this, e);
        oDiv.innerText = parseInt(oDiv.innertext) + 1;
    }
    oBtn.onclick = throttle(buy, 1000)
</script>
```

### 防抖

函数防抖就是在函数需要频繁触发时，只有足够空闲的时间，才执行一次。好像公交司机会等人都上车后才开车一样

```
<input type="text" id="inp"></input>
<script>
	var oInp = document.getElementById('inp');
    function debounce(handler, delay) {
        var timer = null;
        return function () {
            var _self = this,
                _arg = arguments;
            clearTimeout(timer);
            timer = setTimeout(function () {
                ajax.apply(_self, _arg);
            }, delay)
        } 
    }
    
    function ajax(e) {
        // 模拟ajax
        console.log(e, this.value)
    }
    oInp.oninput = debounce(ajax, 2000);


</script>
```

#### [防抖瀑布流图片展示示例](https://excumes.github.io/myDemo/throttle/index.html)



