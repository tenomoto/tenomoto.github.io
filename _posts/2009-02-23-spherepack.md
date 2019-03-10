---
id: 145
title: SPHEREPACK
date: 2009-02-23T23:40:00+09:00
author: takeshi
layout: post
guid: https://www.enomosphere.net/2009/02/23/spherepack/
permalink: /2009/02/23/spherepack/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2007/10/spherepack.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/7711942519961044202
categories:
  - コンピュータ
  - 研究
tags:
  - Fortran
  - g95
  - NCL
---
07/10/06 19:51

[SPHEREPACK](http://www.cisl.ucar.edu/css/software/spherepack/)はLegendre変換をするFortranライブラリ.

Mac OS X上でg95を使ってコンパイルして使っている。

解像度変換のユーティリティルーチンtrssph()が配列サイズが大きいときにNaNを返すことがある。試した範囲では、288×145を1200×600にするのは大丈夫で、1440×720にするのはだめだった。 

メモリ節約のため、trssph()は、Legendre陪関数を逐次計算するサブルーチンsphcom.fにあるlegin()でルジャンドル陪 関数が正しく計算されないようである。アルゴリズムとしては、robustな方法を使っているはずだし、ベクトルのLegendre変換をするルーチンは うまく動作する。また、SPHEREPACKを呼んでいるNCLでは、正しく動作する。

ソースを見たところ、ルジャンドル陪関数を計算するときに必要な係数abel, bbel, cbelが大きな整数のかけ算になっていたためであることが分かった。shagc.f, shsgc.f, shags.f, shsgs.f, shigc.f, shigs.fでは

```diff
-      abel(imn)=sqrt(float((2*n+1)*(m+n-2)*(m+n-3))/
-     1               float(((2*n-3)*(m+n-1)*(m+n))))
-      bbel(imn)=sqrt(float((2*n+1)*(n-m-1)*(n-m))/
-     1               float(((2*n-3)*(m+n-1)*(m+n))))
-      cbel(imn)=sqrt(float((n-m+1)*(n-m+2))/
-     1               float(((n+m-1)*(n+m))))
+      abel(imn)=sqrt((2.*n+1.)*(m+n-2.)*(m+n-3.)/
+     1               ((2.*n-3.)*(m+n-1.)*(m+n)))
+      bbel(imn)=sqrt((2.*n+1.)*(n-m-1.)*(n-m)/
+     1               ((2.*n-3.)*(m+n-1.)*(m+n)))
+      cbel(imn)=sqrt((n-m+1.)*(n-m+2.)/
+     1               ((n+m-1.)*(n+m))) </p>
```

と修正 (diff -uの出力)したところ、問題なく動作した。また`vhags.f`と`vhsgs.f`は以下の通り修正した。

```diff
-      abel = dsqrt(dble(float((2*n+1)*(m+n-2)*(m+n-3)))/
-     1                dble(float((2*n-3)*(m+n-1)*(m+n))))
-      bbel = dsqrt(dble(float((2*n+1)*(n-m-1)*(n-m)))/
-     1                dble(float((2*n-3)*(m+n-1)*(m+n))))
-      cbel = dsqrt(dble(float((n-m+1)*(n-m+2)))/
-     1                dble(float((m+n-1)*(m+n))))
+      abel = dsqrt((2.d0*n+1.d0)*(m+n-2.d0)*(m+n-3.d0)/
+     1                <span style="color: rgb(255, 0, 0);">(</span>(2.d0*n-3.d0)*(m+n-1.d0)*(m+n)<span style="color: rgb(255, 0, 0);">)</span>)
+      bbel = dsqrt((2.d0*n+1.d0)*(n-m-1.d0)*dble(n-m)/
+     1                <span style="color: rgb(255, 0, 0);">(</span>(2.d0*n-3.d0)*(m+n-1.d0)*(m+n)<span style="color: rgb(255, 0, 0);">)</span>)
+      cbel = dsqrt((n-m+1.d0)*(n-m+2.d0)/
+     1 <span style="color: rgb(255, 0, 0);">(</span>(m+n-1.d0)*(m+n)<span style="color: rgb(255, 0, 0);"></span><span style="color: rgb(255, 0, 0);">)</span>)
```

```diff
-      abel = dsqrt(dble(float((n+m)*(n-m+1))))/dcf
-      bbel = dsqrt(dble(float((n-m)*(n+m+1))))/dcf
+      abel = dsqrt((n+m)*(n-m+1.d0))/dcf
+      bbel = dsqrt((n-m)*(n+m+1.d0))/dcf
```
### 2009/2/23 追記

パッチにバグがありました．vhags.fとvhsgs.fの修正の前半，abel, bbel, cbelの分母全体の括弧がありませんでしたので訂正しました．