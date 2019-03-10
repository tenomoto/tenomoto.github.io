---
id: 66
title: GNU enscriptをMacPortsでインストール
date: 2012-01-07T14:33:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2012/01/07/gnu-enscript%e3%82%92macports%e3%81%a7%e3%82%a4%e3%83%b3%e3%82%b9%e3%83%88%e3%83%bc%e3%83%ab/'
permalink: /2012/01/07/gnu-enscript-macports/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2012/01/gnu-enscriptmacports.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/48209023339889933
categories:
  - コンピュータ
tags:
  - Fortran
  - macports
---
新・OS XハッキングでGNU enscriptが紹介されていた．MacPortsで探してみる．
<pre>
$ port search enscript
enscript @1.6.4 (print)
    Replacement for Adobe's 'enscript' program</pre>
variantsを確認．
<pre>
$ port variants enscript
enscript has the variants:
   mediaA4: use A4
   universal: Build for multiple architectures</pre>
+mediaA4を指定した方が良さそうだ．
<pre>
$ sudo port -d install enscript +mediaA4</pre>
デフォルトではF77のみ対応．F90用のファイルを紹介する<a href="http://husky.wordpress.com/2011/05/01/enscript-fortran-90-format/">記事</a>． ~/.enscriptの下に配置．