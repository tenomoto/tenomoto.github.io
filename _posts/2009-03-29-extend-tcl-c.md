---
id: 132
title: C言語でTclを拡張
date: 2009-03-29T12:26:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2009/03/29/c%e8%a8%80%e8%aa%9e%e3%81%a7tcl%e3%82%92%e6%8b%a1%e5%bc%b5/'
permalink: /2009/03/29/extend-tcl-c/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2009/03/ctcl.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/8277175692172274501
categories:
  - コンピュータ
tags:
  - C
  - Tcl
---
Welch, Jones, and Hobbsの<a href="http://www.amazon.co.jp/gp/product/0130385603?ie=UTF8&amp;tag=enomospheddoj-22&amp;linkCode=as2&amp;camp=247&amp;creative=7399&amp;creativeASIN=0130385603">Practical Programming in Tcl and Tk</a>の第47章には，C言語でTclを拡張する方法が説明されている．

Example 47-2にはバグがあり，古い書き方が残っている．
<pre>
interp-&gt;result = "Usage: random ?range?";</pre>
のように直接Tcl_interpのフィールドを操作するのではなく，本文中にあるように
<pre>
Tcl_SetResult(interp, "Usage: random ?range?", TCL_STATIC);</pre>
とした方が安全．

文字列は<code>buffer</code>という名前で宣言しているので，<code>buf</code>は誤り．

リンクオプションは，<code>-bundle</code>でも<code>-dylib</code>でもよい．tclのソースのmacosx/READMEには-dylibのみ<code>unload</code>可能とあるが，どうしたらよいかは分からない．

MacPortsのTclでは，<code>libtcl.dylib</code>にリンクするが，Mac OS X添付のTclでは，<code>-framework Tcl -framework System</code>が使える．自分でソースからコンパイルするときは，ソースのmacosxで<code>./configure</code>のオプションに<code>--enable-framework</code>を付け加える．

ところで，Leopard添付のtclshでは共有ライブラリの読み込みができたが，MacPortsのtcl-8.5.6では<code>Random_SafeInit, Random_SafeUnload, Random_Unload</code>をソースに定義していないとエラーとなる．
<pre>
Random_SafeInit(Tcl_Interp *interp) {
    return Random_Init(interp);
}
int
Random_Unload(Tcl_Interp *interp, int flags) {
    return TCL_OK;
}
int
Random_SafeUnload(Tcl_Interp *interp, int flags) {
    return TCL_OK;
}</pre>
Ubuntuでやってみたが，これらは必要ないので，MacでTcl-8.5を使うときに発生する問題のようだ．

MacPortsの<code>tclsh</code>（tclを+universalでインストール）では，ロード後コマンドを実行したら，<code>malloc</code>でエラーが出た．ActiveTclや/usr/localにインストールしたものは大丈夫だった．MacPortsでも+universal +threadsとしたら，正常に動作するようになった．