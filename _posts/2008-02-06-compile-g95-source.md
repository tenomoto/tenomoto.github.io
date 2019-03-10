---
id: 190
title: ソースからg95をコンパイルする
date: 2008-02-06T15:46:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2008/02/06/%e3%82%bd%e3%83%bc%e3%82%b9%e3%81%8b%e3%82%89g95%e3%82%92%e3%82%b3%e3%83%b3%e3%83%91%e3%82%a4%e3%83%ab%e3%81%99%e3%82%8b/'
permalink: /2008/02/06/compile-g95-source/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2008/02/g95_06.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/2682889964377821196
categories:
  - コンピュータ
tags:
  - g95
---
g95をソースからコンパイルする方法は, g95のサイトに<a href="http://www.g95.org/src.shtml">手順</a>が示されているが要点を下記に記す.

まず, gcc-4.0.3とg95のソースを取得する.
最新のgcc-4.2.xを使うには大規模な改変が必要になる. 当面gcc-4.2系列に移行する予定はないそうである.

gcc-4.0.3を展開し, その中にg95というディレクトリを作る. gcc-4.0.3/g95に移動して,
<blockquote>
<pre>../configure --enable-languages=c</pre>
</blockquote>
のあとmakeする. 必要なファイルlibgcc.a, libbackend.aができればよい.

次にg95を展開して,
<blockquote>./configure --prefix=<span style="color: #006600;">インストール先</span> --with-gcc-dir=<span style="color: #006600;">gccのディレクトリ</span></blockquote>
を実行. <span style="color: #006600;">インストール先</span>には適切なインストール先, 例えば$HOMEを指定する. <span style="color: #006600;">gccのディレクトリ</span>&lt;gccのディレクトリ&gt;は上で使ったgcc-4.0.3を指定する. make, make install (インストール先によっては, 管理者権限が必要な場合がある) した後, libf95.a-0.91.tgz (安定版の場合はlibf95.a-0.90.tgz) を展開して, configure, make, make installする. configureのprefixオプションは, 上と同じインストール先を指定する. 適宜, バイナリファイルの名前はプラットフォームに依存したものになるので, 使いやすいようにシンボリックリンクをはる.


Mac OS X 10.5 (Leopard) では, いくつかパッチが必要になるので, パッケージ管理システムMacPortsまたはFinkからインストールすることを勧める.