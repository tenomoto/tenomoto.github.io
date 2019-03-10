---
id: 4
title: ClangでOpenMP
date: 2014-07-05T17:58:47+09:00
author: takeshi
layout: post
guid: https://www.enomosphere.net/?p=4
permalink: /2014/07/05/clang-openmp/
categories:
  - コンピュータ
tags:
  - clang
  - openmp
---
MacやFreeBSDのデフォルトのコンパイラはclangだが，数値計算ではOpenMPが使えるgccに一日の長がある。ClangでもOpenMPはないのかと思い検索したところ，<a title="OpenMP/Clang" href="http://clang-omp.github.io">OpenMP/Clang</a>があることを知り，試してみた。
<!--more-->

<h2>コンパイラ</h2>
<a title="OpenMP/Clang" href="http://clang-omp.github.io">OpenMP/Clang</a>のGetting the source codeの通りにソースを取得。同BuildingにあるようにClangの<a href="http://clang.llvm.org/get_started.html">Getting Started Building and Running Clang</a>に従ってコンパイル。llvmとclangをコンパイルするので時間がかかるが，Mavericksでは何の問題もなく終了した。buildというディレクトリからconfigureとmakeをすると，build/Debug+Asserts以下にbinとlibができる。
<h2>実行時ライブラリ</h2>
次にIntelの<a href="https://www.openmprtl.org">OpenMP Runtime Library</a>をダウンロード。clangでのビルドに対応しているが，gccを探してバージョンを調べるところでコンパイルが止まってしまう。tools/check-tools.plを編集する。単純に変数$verと$bldを指定した。
<pre>--- tools/check-tools.pl.orig	2013-12-14 03:08:50.000000000 +0900
+++ tools/check-tools.pl	2014-07-05 16:19:31.000000000 +0900
@@ -276,8 +276,10 @@
             # i686-apple-darwin8-gcc-4.0.1 (GCC) 4.0.1 (Apple Computer, Inc. build 5367)
             # i686-apple-darwin9-gcc-4.0.1 (GCC) 4.0.1 (Apple Inc. build 5484)
             # i686-apple-darwin11-llvm-gcc-4.2 (GCC) 4.2.1 (Based on Apple Inc. build 5658) (LLVM build 2336.9.00)
-            $stdout =~ m{^.*? \(GCC\) (\d+\.\d+\.\d+) \(.*Apple.*?Inc\. build (\d+)\)}m;
-            ( $ver, $bld ) = ( $1, $2 );
+#            $stdout =~ m{^.*? \(GCC\) (\d+\.\d+\.\d+) \(.*Apple.*?Inc\. build (\d+)\)}m;
+#            ( $ver, $bld ) = ( $1, $2 );
+            $ver = "4.8.2";
+            $bld = "2";
         } else {
             if ( 0 ) {
             } elsif ( $stdout =~ m{^.*? \(GCC\) (\d+\.\d+\.\d+)(?: (\d+))?}m ) {
</pre>
ちなみにgccはMacPortsのgcc48だが，
<pre>$ sudo port select gcc mp-gcc48
</pre>
としてあるので，一応<code>/opt/local/bin/gcc</code>がある。

もうひとつsrc/makefile.mkで余計なld-flagsをコメントアウトする必要がある。
<pre>--- src/makefile.mk.orig	2013-12-14 03:08:48.000000000 +0900
+++ src/makefile.mk	2014-07-05 16:10:20.000000000 +0900
@@ -430,7 +430,7 @@
 endif
 
 ifeq "$(os)" "mac"
-    ld-flags += -no-intel-extensions
+#    ld-flags += -no-intel-extensions
     ld-flags += -single_module
     ld-flags += -current_version $(VERSION).0 -compatibility_version $(VERSION).0
 endif
</pre>
<pre>$ make compiler=clang
</pre>
とするとtmpの下でコンパイルが実行され，tmp/mac_32e.../libiomp5.dylibができる。ヘッダはexports/common/includeにコピーされる。ライブラリは，exports/libというディレクトリを作りコピーした。
<h2>環境変数の設定</h2>
<a title="OpenMP/Clang" href="http://clang-omp.github.io">OpenMP/Clang</a>のUsingに従って環境変数を設定する。