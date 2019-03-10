---
id: 127
title: GrADSで書いた絵の縞
date: 2009-06-05T12:08:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2009/06/05/grads%e3%81%a7%e6%9b%b8%e3%81%84%e3%81%9f%e7%b5%b5%e3%81%ae%e7%b8%9e/'
permalink: /2009/06/05/artificial-lines-grads/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2009/06/grads.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/9089378187459484392
categories:
  - コンピュータ
tags:
  - GrADS
---
GrADSのメタファイルから作成したEPSには縞が出る．

GrADS:
<pre>
ga-&gt; set gxout shaded

ga-&gt; enable print foo.gx
ga-&gt; print
ga-&gt; dispable print</pre>
コマンドライン:
<pre>
$ gxeps -c -i foo.gx -o foo.eps</pre>
これは，アンチエイリアスが原因．

ImageMagickで縞のないラスタ画像を作るには，
<pre>
convert +antialias foo.eps foo.png</pre>
とする．