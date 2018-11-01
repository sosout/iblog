---
title: 移动端(手机端)页面自适应解决方案—rem布局篇
date: 2018-08-03 22:01:33
tags:
    - rem
categories:
    - 前端教程
---

假设设计妹妹给我们的设计稿尺寸为750 * 1340。结合网易、淘宝移动端首页html元素上的动态font-size属性、设计稿尺寸、前端与设计之间协作流程一般分为下面两种：

### 一、网易做法：
引入：页面开头处引入下面这段代码，用于动态计算font-size

``` js
(function(doc, win) {
	var docEl = doc.documentElement,
	    isIOS = navigator.userAgent.match(/\(i[^;]+;( U;)? CPU.+Mac OS X/),
	    dpr = isIOS ? Math.min(win.devicePixelRatio, 3) : 1,
	    dpr = window.top === window.self ? dpr : 1, //被iframe引用时，禁止缩放
	    dpr = 1,
	    scale = 1 / dpr,
	    resizeEvt = 'orientationchange' in window ? 'orientationchange' : 'resize';
	docEl.dataset.dpr = dpr;
	var metaEl = doc.createElement('meta');
	metaEl.name = 'viewport';
	metaEl.content = 'initial-scale=' + scale + ',maximum-scale=' + scale + ', minimum-scale=' + scale;
	docEl.firstElementChild.appendChild(metaEl);
	var recalc = function() {
	    var width = docEl.clientWidth;
	    if (width / dpr > 750) {
	        width = 750 * dpr;
	    }
	    // 乘以100，px : rem = 100 : 1
	    docEl.style.fontSize = 100 * (width / 750) + 'px';
	};
	recalc()
	if (!doc.addEventListener) return;
	win.addEventListener(resizeEvt, recalc, false);
})(document, window);
```
**使用：**
未引入前：
``` css
body {
	width: 750px;
	height: 640px;
}
```
引入后：除以100并将px换成rem

``` css
body {
	width: 7.5rem;
	height: 6.4rem;
}
```
换算的依据：

``` js
// 乘以100，px : rem = 100 : 1
var recalc = function() {
    var width = docEl.clientWidth;
	if (width / dpr > 750) {
	    width = 750 * dpr;
	}
	// 乘以100，px : rem = 100 : 1
	docEl.style.fontSize = 100 * (width / 750) + 'px';
};
```

### 二、淘宝做法（推荐做法，尤其是app内嵌页面）：
引入：页面开头处引入下面这段代码，用于动态计算font-size，或者单独放入一个文件，引入文件也可以

``` js
;
(function(win, lib) {
    var doc = win.document;
    var docEl = doc.documentElement;
    var metaEl = doc.querySelector('meta[name="viewport"]');
    var flexibleEl = doc.querySelector('meta[name="flexible"]');
    var dpr = 0;
    var scale = 0;
    var tid;
    var flexible = lib.flexible || (lib.flexible = {});

    if (metaEl) {
        var match = metaEl.getAttribute('content').match(/initial\-scale=([\d\.]+)/);
        if (match) {
            scale = parseFloat(match[1]);
            dpr = parseInt(1 / scale);
        }
    } else if (flexibleEl) {
        var content = flexibleEl.getAttribute('content');
        if (content) {
            var initialDpr = content.match(/initial\-dpr=([\d\.]+)/);
            var maximumDpr = content.match(/maximum\-dpr=([\d\.]+)/);
            if (initialDpr) {
                dpr = parseFloat(initialDpr[1]);
                scale = parseFloat((1 / dpr).toFixed(2));
            }
            if (maximumDpr) {
                dpr = parseFloat(maximumDpr[1]);
                scale = parseFloat((1 / dpr).toFixed(2));
            }
        }
    }

    if (!dpr && !scale) {
        var isAndroid = win.navigator.appVersion.match(/android/gi);
        var isIPhone = win.navigator.appVersion.match(/iphone/gi);
        var devicePixelRatio = win.devicePixelRatio;
        if (isIPhone) {
            // iOS下，对于2和3的屏，用2倍的方案，其余的用1倍方案
            if (devicePixelRatio >= 3 && (!dpr || dpr >= 3)) {
                dpr = 3;
            } else if (devicePixelRatio >= 2 && (!dpr || dpr >= 2)) {
                dpr = 2;
            } else {
                dpr = 1;
            }
        } else {
            // 其他设备下，仍旧使用1倍的方案
            dpr = 1;
        }
        scale = 1 / dpr;
    }

    docEl.setAttribute('data-dpr', dpr);
    if (!metaEl) {
        metaEl = doc.createElement('meta');
        metaEl.setAttribute('name', 'viewport');
        metaEl.setAttribute('content', 'initial-scale=' + scale + ', maximum-scale=' + scale + ', minimum-scale=' + scale + ', user-scalable=no');
        if (docEl.firstElementChild) {
            docEl.firstElementChild.appendChild(metaEl);
        } else {
            var wrap = doc.createElement('div');
            wrap.appendChild(metaEl);
            doc.write(wrap.innerHTML);
        }
    }

    function refreshRem() {
        var width = docEl.getBoundingClientRect().width;
        // 适配平板
        if (width / dpr > 540) {
            width = 540 * dpr;
        }
        var rem = width / 10;
        docEl.style.fontSize = rem + 'px';
        flexible.rem = win.rem = rem;
    }

    win.addEventListener('resize', function() {
        clearTimeout(tid);
        tid = setTimeout(refreshRem, 300);
    }, false);
    win.addEventListener('pageshow', function(e) {
        if (e.persisted) {
            clearTimeout(tid);
            tid = setTimeout(refreshRem, 300);
        }
    }, false);

    if (doc.readyState === 'complete') {
        doc.body.style.fontSize = 12 * dpr + 'px';
    } else {
        doc.addEventListener('DOMContentLoaded', function(e) {
            doc.body.style.fontSize = 12 * dpr + 'px';
        }, false);
    }


    refreshRem();

    flexible.dpr = win.dpr = dpr;
    flexible.refreshRem = refreshRem;
    flexible.rem2px = function(d) {
        var val = parseFloat(d) * this.rem;
        if (typeof d === 'string' && d.match(/rem$/)) {
            val += 'px';
        }
        return val;
    }
    flexible.px2rem = function(d) {
        var val = parseFloat(d) / this.rem;
        if (typeof d === 'string' && d.match(/px$/)) {
            val += 'rem';
        }
        return val;
    }

})(window, window['lib'] || (window['lib'] = {}));
```
**使用：**

未引入前：

``` css
body {
	width: 750px;
	height: 640px;
}
```
引入后：

``` less
@font-size-base: 75;
body {
	width: 750rem/@font-size-base;
	height: 640rem/@font-size-base;
}
```
换算依据：

``` js
function refreshRem() {
    var width = docEl.getBoundingClientRect().width;
    // 适配平板
    if (width / dpr > 540) {
        width = 540 * dpr;
    }
    var rem = width / 10;
    docEl.style.fontSize = rem + 'px';
    flexible.rem = win.rem = rem;
}
```

这边是用的less，如果您没有用less，就需要手动计算，当然也可以转化为px : rem = 100 : 1。
如果想转化为px : rem = 100 : 1，可以修改上面的refreshRem函数：

``` js
function refreshRem() {
    var width = docEl.getBoundingClientRect().width
    // 适配平板
    if (width / dpr > 750) {
      width = 750 * dpr
    }
    var rem = 100 * (width / 750)
    docEl.style.fontSize = rem + 'px'
    flexible.rem = win.rem = rem;
}

```
**使用：**

未引入前：
 
``` css
body {
	width: 750px;
	height: 640px;
}
```
引入后：除以100并将px换成rem

``` css
body {
	width: 7.5rem;
	height: 6.4rem;
}
```
换算依据就是上面修改的代码：

``` js
function refreshRem() {
    var width = docEl.getBoundingClientRect().width
    // 适配平板
    if (width / dpr > 750) {
      width = 750 * dpr
    }
    var rem = 100 * (width / 750)
    docEl.style.fontSize = rem + 'px'
    flexible.rem = win.rem = rem;
}
```
