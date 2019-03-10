---
id: 237
title: TclをMac OS Xにインストール
date: 2006-12-19T18:05:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2006/12/19/tcl%e3%82%92mac-os-x%e3%81%ab%e3%82%a4%e3%83%b3%e3%82%b9%e3%83%88%e3%83%bc%e3%83%ab/'
permalink: /2006/12/19/install-tcl-mac-os-x/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2006/12/tclmac-os-x.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/6342438745854304662
categories:
  - コンピュータ
tags:
  - Tcl
---
<div>

tcl/tkは多くのプラットフォームで利用できますが、ここではMac OS Xでのインストールを紹介します。
<h4>OS添付のもの</h4>
Mac OS X には、Tclが最初からインストールされています。tclshは、/usr/binにあり、ヘッダやライブラリはそれぞれ/usr/include, /usr/libにシンボリック・リンクがあります。本体は、/System/Library/Frameworks/Tcl.famework以下にあ ります。
<h4>Fink</h4>
X-Window用のtcl/tkがFinkからインストールできます <a href="http://fink.sourceforge.net/pdb/package.php/tcltk">[tcl/tk/Fink]</a>。
<h4>TclTkAqua</h4>
Carbonを使ってAquaインターフェースを実現したWishを含むのが、<a href="http://tcltkaqua.sourceforge.net/">TclTkAqua</a>です。Batteries Includedは、50ものエクステンションを含んでいます。
<h4>ソースからのビルド</h4>
ソースからのビルドも、非常に簡単です。tcl、tkともmacosxディレクトリに移動しmakeするだけです。デフォルトのターゲットは、/usr/localで/Library/Frameworks以下にもフレームワークがインストールされます。

</div>