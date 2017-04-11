---
layout: post
title: 奇葩BUGs-Python
category : 写代码
tagline: "Supporting tagline"
tags : [Python, Bugs]
---
{% include JB/setup %}

**收集一些Python开发过程中遇到过的坑**


> 2017-04-11

安装numpy 报如下错

```
IOError: [Errno 13] Permission denied: 'xxxx\multiarray.pyd'
```

基本原因是安装过程中python还在跑，所以基本上只要把IDE（IPython, Eclipse, Pycharm之类的）都关掉，重新安装即可！
