---
id: 29
title: SwiftでPLplot
date: 2014-08-02T12:26:19+09:00
author: takeshi
layout: post
guid: https://www.enomosphere.net/?p=29
permalink: /2014/08/02/swift-plplot/
categories:
  - コンピュータ
tags:
  - PLplot
  - Swift
---
PLplotの最初の<a href="http://plplot.sourceforge.net/examples.php?demo=00">例</a>をSwiftに移植してみた。<!--more-->

<a href="https://www.enomosphere.net/wp-content/uploads/2014/08/simple.png"><img class="alignnone size-medium wp-image-499" src="https://www.enomosphere.net/wp-content/uploads/2014/08/simple-300x225.png" alt="simple" width="300" height="225" /></a>

プリプロセッサでの#defineは，定数には対応しているが別名には対応していないようで，pl*()ではなくc_pl*()を直接書く必要がある。PLINTはInt32なので，配列の要素数はInt()で型変換する必要がある。コマンドライン引数argc, argvは，SwiftではC_ARGC，C_ARGVかProcess.argumentsで<a href="http://stackoverflow.com/questions/24110731/how-to-i-access-argv-and-argc-in-swift">参照できる</a>。Process.argumentsは[String]を，C_ARGVはUnsafePointer&lt;Int8&gt;を返すので，どちらかをUnsafeMutablePointer()でキャストして渡す。
<h3>main.swift</h3>
<pre>let n: PLINT = 101
let xmin: PLFLT = 0.0; let xmax: PLFLT = 1.0
let ymin: PLFLT = 0.0; let ymax: PLFLT = 100.0
var x = [PLFLT](count: Int(n), repeatedValue: 0.0)
var y = [PLFLT](count: Int(n), repeatedValue: 0.0)
for (index, value) in enumerate(x) {
 x[index] = PLFLT(index) / (PLFLT(n) - 1)
 y[index] = ymax * x[index] * x[index]
}
var argc: Int32 = Int32(C_ARGC)
c_plparseopts(&amp;argc, UnsafeMutablePointer(C_ARGV), PL_PARSE_FULL)
c_plinit()
c_plenv(xmin, xmax, ymin, ymax, 0, 0)
c_pllab("x", "y=100 x#u2#d", "Simple PLplot demo of a 2D line plot")
c_plline(n, x, y)
c_plend()</pre>
<h3>Makefile</h3>
<pre>SWIFT = /usr/bin/xcrun swiftc
CPPFLAGS = -I/usr/include -I/opt/local/include/plplot
LDFLAGS = -L/opt/local/lib -lplplotd
TARGET = simple
OBJS = main.o
HDRS = $(TARGET).h

$(TARGET) : $(OBJS)
	$(SWIFT) $(LDFLAGS) $^ -o $@

%.o : %.swift
	$(SWIFT) $(CPPFLAGS) -c $&lt; -import-objc-header $(HDRS)

clean :
	rm $(TARGET) $(OBJS)
</pre>