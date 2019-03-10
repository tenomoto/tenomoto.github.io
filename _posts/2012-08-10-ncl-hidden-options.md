---
id: 50
title: NCLの隠しオプション
date: 2012-08-10T09:30:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2012/08/10/ncl%e3%81%ae%e9%9a%a0%e3%81%97%e3%82%aa%e3%83%97%e3%82%b7%e3%83%a7%e3%83%b3/'
permalink: /2012/08/10/ncl-hidden-options/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2012/08/ncl.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/5194843701004729375
categories:
  - コンピュータ
tags:
  - NCL
---
NCLを-hオプションを付けて起動させれば，オプション一覧が表示される。<!--more-->
<pre>$ ncl -h
Usage: ncl -hnpxV  
  -n: don't enumerate values in print()
  -p: don't page output from the system() command
  -o: retain former behavior for certain backwards-incompatible changes
  -x: echo NCL commands
  -V: print NCL version and exit
  -h: print this message and exit</pre>
ソース<code>ncl_ncarg-6.0.0/ni/src/ncl/Ncl.c</code>を読むと， 二つの隠しオプションがあることが分る。
<pre>            /* NOT ADVERTISED!  Will override "no echo" and print EVERYTHING! */
            case 'X':
                NCLoverrideEcho = 1;
                break;

            /* NOT ADVERTISED!  Will not echo copyright notice! */
            case 'Q':
                NCLnoCopyright = 1;
                break;</pre>
-Xは何でも書き出すオプションで，デバッグ時に有効。-Qはコピーライトを表示しない。-nQとすれば，nclで計算したデータをテキストに書き出すときに便利。