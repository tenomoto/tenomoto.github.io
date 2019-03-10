---
id: 136
title: C++で動的配列
date: 2009-03-09T19:59:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2009/03/09/c%e3%81%a7%e5%8b%95%e7%9a%84%e9%85%8d%e5%88%97/'
permalink: /2009/03/09/cxx-dynamic-array/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2009/03/c_9204.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/571520664451763444
categories:
  - コンピュータ
tags:
  - CXX
---
Cのmallocを使ってもいいが，C++ではnew演算子を使う．
<pre>float* x = new float[n];</pre>
配列は，やっぱりFortranが便利．