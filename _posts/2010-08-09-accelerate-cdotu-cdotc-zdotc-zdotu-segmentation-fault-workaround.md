---
id: 86
title: Accelerateのcdotu, cdotc, zdotc, zdotuで出るsegmentation faultを回避する
date: 2010-08-09T22:17:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2010/08/09/accelerate%e3%81%aecdotu-cdotc-zdotc-zdotu%e3%81%a7%e5%87%ba%e3%82%8bsegmentation-fault%e3%82%92%e5%9b%9e%e9%81%bf%e3%81%99%e3%82%8b/'
permalink: /2010/08/09/accelerate-cdotu-cdotc-zdotc-zdotu-segmentation-fault-workaround/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2010/08/acceleratecdotu-cdotc-zdotc.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/3764943708735503034
categories:
  - コンピュータ
tags:
  - Accelerate
  - g95
  - LAPACK
  - Mac
  - Octave
---
MacPortsのOctaveがATLASに移行してしまい, Accelerateを使わなくなった.
ATLASはコンパイルに時間がかかる上, g95がサポートされていない.
ATLASがg95サポートするようにしてもよいのだが, OSに添付され最適化されているAccelerate frameworkを使いたい.
そこでAccelerateを<a href="http://trac.macports.org/ticket/21797">復活</a>させようとしている.

問題となるのは, OctaveのconfigureでCDOTU, ZDOTUのテストにSegmentation faultなどが出て失敗することである.

<a href="http://developer.apple.com/hardwaredrivers/ve/errata.html#fortran_conventions">原因</a>は, AccelerateはCBLASなのでCやg77のABIに従い, 返り値が複素数を指すポインタであるのに, g95, gfortranは浮動小数点レジスタファイルであること. gfortranでは-ff2cとすることで解決する. g95ではラッパが必要. Appleが示したラッパをちょっとだけ改変して関数名に_をつけたので, ラッパは-fno-underscoringをつけてコンパイルするが, 呼び出し側ではオプションは不要.

2010-11-20追記: githubにて<a href="https://github.com/tenomoto/dotwrp">公開</a>. MacPortsを使ってインストール<a href="http://svn.macports.org/repository/macports/trunk/dports/math/dotwrp/Portfile">可</a>．
<pre>
!g95 -fno-underscoring dotwrp.f90 -c
double complex function zdotc_(n, zx, incx, zy, incy)
double complex zx(*), zy(*), z
integer n, incx, incy

call cblas_zdotc_sub(%val(n), zx, %val(incx), zy, %val(incy), z)

zdotc_ = z
return
end

double complex function zdotu_(n, zx, incx, zy, incy)
double complex zx(*), zy(*), z
integer n, incx, incy

call cblas_zdotu_sub(%val(n), zx, %val(incx), zy, %val(incy), z)

zdotu_ = z
return
end

complex function cdotc_(n, cx, incx, cy, incy)
complex cx(*), cy(*), c
integer n, incx, incy

call cblas_cdotc_sub(%val(n), cx, %val(incx), cy, %val(incy), c)

cdotc_ = c
return
end

complex function cdotu_(n, cx, incx, cy, incy)
complex cx(*), cy(*), c
integer n, incx, incy

call cblas_cdotu_sub(%val(n), cx, %val(incx), cy, %val(incy), c)

cdotu_ = c
return
end</pre>