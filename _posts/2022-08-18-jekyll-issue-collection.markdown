---
layout: post
title:  "jekyll 问题汇总"
date:   2022-08-18 16:22:05 +0800
last-updated-date:   2022-08-23 14:55:01 +0800
image:  21.jpg
tags:   dev jekyll
---

jekyll 问题汇总
--------------------

- [jekyll 问题汇总](#jekyll-问题汇总)
    - [#01 Issue: Jekyll 运行的时候提示错误 cannot load such file -- webrick (LoadError)](#01-issue-jekyll-运行的时候提示错误-cannot-load-such-file----webrick-loaderror)
    - [#02 How to: Show double quotes on page title - 文章标题显示双引号](#02-how-to-show-double-quotes-on-page-title---文章标题显示双引号)
    - [#03 How to: Show mult-line content in yaml\jekyll - 在 Jekyll (yaml 格式) 的配置信息中保存多行文本内容](#03-how-to-show-mult-line-content-in-yamljekyll---在-jekyll-yaml-格式-的配置信息中保存多行文本内容)
   


---
#### #01 Issue: Jekyll 运行的时候提示错误 cannot load such file -- webrick (LoadError)
**Symptom:**  
错误详情没截 :(

**Solution:**  
根据官方的项目的说明, 从 [Ruby 3.0](https://www.ruby-lang.org/en/news/2020/12/25/ruby-3-0-0-released/) 开始 webrick 已经不在绑定到 Ruby 中了。
webrick 需要手动进行添加。添加的命令为：
```
bundle add webrick
```
之后就可以解决这个问题了。

**ref:**  
[Jekyll 运行的时候提示错误 cannot load such file -- webrick (LoadError)](https://www.cnblogs.com/huyuchengus/p/15473035.html)

---
#### #02 How to: Show double quotes on page title - 文章标题显示双引号
**Symptom:**  
Wanna show double quotes in the title  
想在 Post 的文章标题里显示双引号

**Solution:**  
![一图胜千言](/images/2022/0818-01.png)

**ref:**  
[Jekyll YAML issue in rendering ""](https://stackoverflow.com/questions/31784058/jekyll-yaml-issue-in-rendering)

---
#### #03 How to: Show mult-line content in yaml\jekyll - 在 Jekyll (yaml 格式) 的配置信息中保存多行文本内容
**Symptom:**  
Wanna show mult-line content in yaml\jekyll  
想在在 Jekyll (yaml 格式) 的配置信息中 （如 description） 保存多行文本内容

**Solution:**  
Yaml syntax for multi-line strings is this one:
```
body: |
  This is a multi-line string.
  "special" metacharacters may
  appear here. The extent of this string is
  indicated by indentation. 
```
Notice that the ==first== line must be an ==space== followed by the | character and a new line. Then you must ==indent== the text one level more than its parent.  
注意第一行 | 的左边要加空格，多行文本内容要加缩进。

**ref:**  
[Jekyll/Liquid - how to add large blocks of text to YAML front matter?](https://stackoverflow.com/questions/6734955/jekyll-liquid-how-to-add-large-blocks-of-text-to-yaml-front-matter)

---