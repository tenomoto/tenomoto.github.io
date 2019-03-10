---
id: 102
title: 英語の月名
date: 2009-12-07T14:51:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2009/12/07/%e8%8b%b1%e8%aa%9e%e3%81%ae%e6%9c%88%e5%90%8d/'
permalink: /2009/12/07/monthname/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2009/12/blog-post.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/2712517531331164972
categories:
  - コンピュータ
tags:
  - sh
---
数字の月名を英語の月名に置き換えるとき配列があると便利だが，/bin/shには無い. caseで書くのも面倒．

通常使われる<a href="http://www.mogami.com/unix/sh-array.html">テクニック</a>．
<pre>
set dummy JAN FEB MAR APR MAY JUN JUL AUG SEP OCT NOV DEC
shift $i
moneng=$1</pre>
dateコマンドを使ったもの．
<pre>
moneng=`LANG=C date -j -f "%m" $mon "+%b" | tr "[:lower:]" "[:upper:]"`</pre>