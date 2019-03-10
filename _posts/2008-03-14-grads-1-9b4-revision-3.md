---
id: 184
title: grads 1.9b4 revision 3
date: 2008-03-14T00:33:00+09:00
author: takeshi
layout: post
guid: https://www.enomosphere.net/2008/03/14/grads-1-9b4-revision-3/
permalink: /2008/03/14/grads-1-9b4-revision-3/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2008/03/grads-19b4-revision-3.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/5228333657535369018
categories:
  - コンピュータ
tags:
  - GrADS
---
同僚がついにiMac G5への移行を開始。

PowerPCなので、g95に必要なodcctoolsのコンパイルがうまくいかないのではと思ったが、odcctoolsはLeopardでは不要だったので、問題なくg95がインストールできた。


gradsのインストールをしていたので、gradsのPortfileを見直したところ、/usr/includeや/usr/libを参照していて美しくない。いろいろと手を入れた。

* zlibを使っていたようなので、zlibへの依存を記述。
* libwmfはprintimの時だけに必要なので、ベタ書きされていたのを削除。
* パッチに.diffの拡張子をつけた。
* Finkのパッケージを参考にして、gx.hにある/usr/localにべた書きで参照しているところを${prefix}に変更。
* gxhpng.cにgcCompareInt()中身がないので、Redhatのパッケージを参考にして中身を記述。
* hdf4に対応。hdf4パッケージもコミット。