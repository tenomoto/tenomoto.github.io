---
id: 41
title: EPSのBoundingBox
date: 2013-02-14T14:29:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2013/02/14/eps%e3%81%aeboundingbox/'
permalink: /2013/02/14/eps-boundingbox/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2013/02/epsboundingbox.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/1537383163645316440
categories:
  - コンピュータ
tags:
  - ghostscript
  - macports
  - NCL
---
nclが生成するepsのBoundingBoxは，<a href="http://www.ncl.ucar.edu/Applications/resize.shtml">レターサイズに固定</a>されている（追記あり）。<!--more-->

エディタでepsファイルを見てみると，
<pre>%%BoundingBox: 0 40 612 758</pre>
となっている。gsnMaximizeを指定していも，縦または横に余分な空白が空いてしまう。そこで，BoundingBoxを再計算して，空白を除去したい。

ghostscriptを使うと，BoundingBoxを計算できる。
<pre>gs -dNOPAUSE -dBATCH -q -sDEVICE=bbox foo.eps 
%%BoundingBox: 199 39 415 756
%%HiResBoundingBox: 199.569017 39.991077 414.431003 755.821032</pre>
これらの数値をepsファイルの中の値と置き換えればよい。自動でやってくれるスクリプトを探したところ，
<ul>
 	<li><a href="http://pages.cs.wisc.edu/~ghost/gsview/epstool.htm">epstool</a>: ghostscriptと同じ作者</li>
 	<li>epscrop: TeX-archiveにシェルスクリプト</li>
 	<li><a href="http://www.scharrer-online.de/attachment/wiki/Software/Perl/fixbb/fixbb">fixbb</a>: Perlスクリプト</li>
</ul>
が見つかった。epstoolはプレビューも付けてくれるので，これがよさそうだ。MacPortsでもインストールできる。

追記: gsn_panelを使わない場合は，適切なBoundingBoxが計算されていた。