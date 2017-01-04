---
layout: post
title: 快速给一堆PDF创建WordCloud
category : 写代码
tagline: "Supporting tagline"
tags : [教程, Python]
---
{% include JB/setup %}

**故事是这样的，年底的某一天，老板让我在某组织的月会里分享一下之前某个月参加某学术会议的经历。在准备的过程中，突发奇想，要是能基于会议的所有paper搞一个WordCloud，不就能很清楚地告诉大家这个会里的小伙伴都是在搞啥！**

虽然时间紧任务重，说做就做！

首先，想起来流程很简单，先从所有pdf抽取word，再统计词频，最后用一个能根据权重生成WordCloud的库就搞定收工了！

摆一张最后效果图先！

<img src="http://i.imgur.com/lvJgFkU.png" width="100%">

**无奖竞猜，这是什么会！**

### 第一步：抽取Word

既然时间紧任务重，很自然地去找别人造好的轮子。

> Word Frequency from PDFs<br/>
> [http://pinkyslemma.com/2013/07/02/word-frequency-from-pdfs/](http://pinkyslemma.com/2013/07/02/word-frequency-from-pdfs/ "Word Frequency from PDFs")

```python
import os
import glob

from pdfminer.pdfinterp import PDFResourceManager, process_pdf
from pdfminer.converter import TextConverter
from pdfminer.layout import LAParams
from cStringIO import StringIO
 
def convert_pdf(path):
 
    rsrcmgr = PDFResourceManager()
    retstr = StringIO()
    codec = 'utf-8'
    laparams = LAParams()
    laparams.all_texts = True
    device = TextConverter(rsrcmgr, retstr, codec=codec, laparams=laparams)
 
    fp = file(path, 'rb')
    process_pdf(rsrcmgr, device, fp)
    fp.close()
    device.close()
 
    str = retstr.getvalue()
    retstr.close()
    return str
 
pdflist = glob.glob("C:\\PATH_TO_PDFS\\*.pdf")
 
for pdf in pdflist:
    print("Working on: " + pdf + '\n')
    fout = open('pdfs.txt','a')
    fout.write(convert_pdf(pdf))
    fout.close()
```

这个过程中，很大机会会报错： 

	pdfminer ImportError: cannot import name process_pdf

这是因为新版的pdfminer已经不支持process_pdf了，当然有对应的对策，参考如下！

> 解决pdfminer ImportError: cannot import name process_pdf<br/>
> [http://blog.csdn.net/mrlevo520/article/details/52136414](http://blog.csdn.net/mrlevo520/article/details/52136414 "解决pdfminer ImportError: cannot import name process_pdf")

### 第二步：统计词频

下一步就是把挖出来的Word进行词频统计，并导出为合适的格式，继续参考轮子！

> Word Frequency from PDFs <br/>
> [http://pinkyslemma.com/2013/07/02/word-frequency-from-pdfs/](http://pinkyslemma.com/2013/07/02/word-frequency-from-pdfs/ "Word Frequency from PDFs")

```python
from collections import Counter
import string
 
fin = open('pdfs.txt','r')
words = fin.read().lower()
out = words.translate(string.maketrans("",""), string.punctuation)
fin.close()
 
wordss = out.split()
 
cnt = Counter(wordss)
 
fout = open('counts.txt','w')
for k, v in cnt.items():
    fout.write(v + "\t" + str(k) + '\n')
fout.close()
```
参照第三步我们会用到的工具，我们把导出的格式设置为：出现次数TAB词。

### 第三步：生成WordCloud

最后一步就是基于我们生成的词频信息生成WordCloud。当然生成之前，需要在上一步导出的词频记录中排除掉无意义的词（比如 the，before，after等）及低频的词，然后直接利用一些在线工具生成WordCloud。当然，这里需要工具能支持词频作为权重调整字体大小。

> HTML5 Word Cloud <br/>
> [https://timdream.org/wordcloud/](https://timdream.org/wordcloud/ "HTML5 Word Cloud")

类似的工具有很多，当然技术党也可以自己搭一个自己的版本，但是还是那句话，时间紧，任务重！

再上一张效果图，猜出来是什么会了么 :)

<img src="http://i.imgur.com/lvJgFkU.png" width="100%">
