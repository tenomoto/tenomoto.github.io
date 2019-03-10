---
id: 85
title: atlasなしのoctave
date: 2010-09-12T21:14:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2010/09/12/atlas%e3%81%aa%e3%81%97%e3%81%aeoctave/'
permalink: /2010/09/12/atlasless-octave/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2010/09/atlasoctave.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/4729822334439274777
categories:
  - コンピュータ
tags:
  - macports
  - Octave
---
Accelerate.frameworkには，<a href="/2010/08/09/accelerate-cdotu-cdotc-zdotc-zdotu-segmentation-fault-workaround/">問題</a>があるために，octaveは行列ライブラリとしてatlasに依存させている．

atlasはコンパイルに時間がかかる上に, g95のvariantがない．gcc44のコンパイルも加えると，かなり長い時間かかる．

そこでarpack, octave用にパッチを作成した．
<ul>
<ul>
 	<li><a href="http://trac.macports.org/ticket/25186">arpack用</a></li>
</ul>
</ul>
&nbsp;
<ul>
<ul>
 	<li><a href="http://trac.macports.org/ticket/21797">octave用</a></li>
</ul>
</ul>
2010-11-21追記: mkoctfileがうまくいかなかった問題を修正.
octaveのビルド中に一時的なディレクトリに生成されるdotwrp.oへの
パスが残ってしまった.
以下のラッパは独立したportとしたので, 下記にあるように,
filesに入れておく必要はない.

g95を使う場合は, octaveのPortfileパッチをあてるだけでなく，
filesの中にdotwrp.f90を入れておく必要がある．

gfortranの場合は
<pre>
sudo port -d install octave +no_atlas</pre>
g95の場合は
<pre>
sudo port -d install octave +g95</pre>
とする．