---
title: rename
date: 2016-08-24 20:16:56
tags:
---

 设计师做了这样命名的logo
   ![银行原图](/images/blogImage/银行原图.png)
   
  为了效率 
  首先想到shell script 批量处理
  后来发现 homebrew 有 rename
  
#   rename 's/\.png/\@3x.png/' *

就变成了
   ![银行改后图](/images/blogImage/银行改后图.png)

