---
id: 544
title: Return complex from C to Fortran
date: 2014-10-05T11:20:36+09:00
author: takeshi
layout: post
guid: https://www.enomosphere.net/?p=544
permalink: /2014/10/05/return_complex_from_c_to_fortran/
categories:
  - コンピュータ
tags:
  - C
  - Fortran
  - macports
---
I wrote a wrapper in Fortran called <a href="https://github.com/tenomoto/dotwrp">dotwrp</a> to avoid the problems in Accelerate (more specifically vecLib) framework (related <a title="Accelerateのcdotu, cdotc, zdotc, zdotuで出るsegmentation faultを回避する" href="https://www.enomosphere.net/2010/08/09/accelerate%e3%81%aecdotu-cdotc-zdotc-zdotu%e3%81%a7%e5%87%ba%e3%82%8bsegmentation-fault%e3%82%92%e5%9b%9e%e9%81%bf%e3%81%99%e3%82%8b/">post</a> in Japanese).<!--more-->

I <a href="https://github.com/tenomoto/dotwrp/commit/d5816854fd4e97e44fe82bca519e1f174dd17408">merged</a> the pull request from <a href="https://github.com/mcg1969">mcg1969</a> who contributed C version of dotwrp several months ago. He created a more capable package called <a title="vecLibFort" href="https://github.com/mcg1969/vecLibFort">vecLibFort</a>. I created a <a href="https://svn.macports.org/repository/macports/trunk/dports/devel/vecLibFort/">port</a> of vecLibFort for MacPorts.

vecLibFort works fine on various version of OS X from Snow Leopard through Mavericks. However I encountered a problem on a PowerPC machine running Leopard. It is dated but I still use it because it is a big endian machine and I need Octave and ncl.

The problem is the one I solved with dotwrp in four years ago: complex return value. I get segfault when linked against the C wrapper but I don't when linked against the Fortran wrapper.

After some Google searches I realize that the returning a struct is involved and <a href="http://concatenative.org/wiki/view/FFI/StructReturns">architecture dependent</a>. I noticed that the use of C99 complex types solves the problem.

C function works on Intel but fails on PPC:
<pre>fcplx addtwoc_(const fcplx *x, const fcplx *y)
{
  fcplx z;
  z.r = x-&gt;r + y-&gt;r;
  z.i = x-&gt;i + y-&gt;i;
  return z;
}
</pre>
Modified C function works on both
<pre>#include 
float complex addtwoc_(const float complex *x, const float complex *y)
{
  float complex z;
  z = *x + *y;
  return z;
}
</pre>
The caller program in Fortran
<pre>      program main

        complex x, y, z, addtwoc
        x = (1.0, 2.0)
        y = (2.0, 2.0)
        z = addtwoc(x, y)
        print *, "z = ", z, " x+y=", x+y
       
      end
</pre>
&nbsp;