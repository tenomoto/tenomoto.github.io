---
id: 186
title: 正弦曲線を描く
date: 2008-02-17T19:58:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2008/02/17/%e6%ad%a3%e5%bc%a6%e6%9b%b2%e7%b7%9a%e3%82%92%e6%8f%8f%e3%81%8f/'
permalink: /2008/02/17/sin-curve-fortran-plplot/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2008/02/blog-post_17.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/8276126430832600889
categories:
  - コンピュータ
tags:
  - Fortran
  - g95
  - PLplot
---
計算結果を可視化するために, Javaを使って数値計算を教えようとする教科書を見かけた.<!--more--> Fortran用の可視化ライブラリはたくさんあるので, Fortranでも計算結果は簡単に可視化できる. アルゴリズムの研究にはJavaでもいいかもしれないが, ゆくゆくは大きな計算をするのならばやはりFortranを使った方がよいと思う.

計算するプログラムと可視化するプログラムは別であることも多く, 言語は同じである必要はない.

ともかく, Fortranから可視化ライブラリを呼んで実際に図を書いてみることにする. PLplotはC (もとはFortran 77) で書かれた可視化ライブラリである. C++, Fortran, Java, Tclなど多数の言語から使える. PLplotを使って, 正弦曲線を描いてみよう.

まずはMacPortsを使ってplplotをインストール.
<blockquote>sudo -d install plplot +g95</blockquote>
正弦曲線を描くプログラムは次の通り.
<pre>program p01
  use plplot, pi=&gt;pl_pi
  implicit none

  integer, parameter :: n = 20
  integer :: i

  real(kind=plflt), dimension(n) :: x, y

  do i=1, n
    x(i) = -pi + 2*pi*(i-1)/(n-1)
    y(i) = sin(x(i))
  end do


  call plinit()
  call plenv(-pi, pi, -1._plflt, 1._plflt, 0, 1)
  call pllab("x", "y", "plot 1 y = sin(x)")
  call plline(x, y)
  call plend()

end program p01</pre>
必要なライブラリをpkg-configで取得してコンパイル.
<pre>g95 p01.f90 `pkg-config --cflags --libs plplotd-f95`</pre>
実行すると, 出力先の選択肢が示される. X Windowに表示するには1を選ぶ.
ほかの番号を選んで, PostScriptやPNG形式で保存することもできる.