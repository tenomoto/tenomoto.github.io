---
id: 653
title: C++ではコンテナを渡してはいけないらしい
date: 2016-05-27T19:11:28+09:00
author: takeshi
layout: post
guid: https://www.enomosphere.net/?p=653
permalink: /2016/05/27/cxx-iterator/
categories:
  - コンピュータ
tags:
  - CXX
---
経度のように周期的なデータが長さ<code>n</code>配列xに格納されているとする。添字が0から始まるとして，<code>x[n]</code>は<code>x[0]</code>，<code>x[-1]</code>は<code>x[n-1]</code>の値を返すようにしたい。<code>[]</code>の定義は後回しにして，今回は関数を書いてみる。
<!--more-->

C++で<code>template</code>を使っておけば，特定の型に依存しないようにするジェネリックプログラミングだと思っていた。しかしC由来の普通の配列には使えない。そもそもコンテナを渡したり，返したりすると，一般性や効率が損なわれるので<a href="http://www.cs.northwestern.edu/~riesbeck/programming/c++/stl-iterators.html">ご法度</a>とのこと。

反復子を渡すようにして，負でもコンテナのサイズより大きくても良い添字<code>i</code>での値を返すジェネリックな関数を書いてみた。

https://gist.github.com/tenomoto/79f5fb60783d24dcb8bf7910da4052c6

ある値以上になる添字を返す関数は，次のように書いたらよさそうだ。

https://gist.github.com/tenomoto/17ff04f4a1445302bb19a439c8c2546b

反復子として，ベクトルは<code>x.cbegin()</code>と<code>x.cend()</code>があるが，<code>valarray</code>にはないので<code>std::begin(x)</code>と<code>std::end(x)</code>を使う。配列はポインタ演算<code>x</code>と<code>x + n</code>（<code>n</code>は配列の長さ）でよい。