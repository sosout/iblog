---
title: 揭秘 http 
tags:
  - http
categories:
  - javascript
date: 2018-10-30 11:34:58
---

### options 请求
当我们的 ajax 的请求为非简单请求时，浏览器会进行预检，即发送 OPTIONS 请求到服务器，询问是否允许跨域。如果响应中允许我们预检请求的跨域行为，则浏览器会进行真正的请求。否则，会报 405 错误。
