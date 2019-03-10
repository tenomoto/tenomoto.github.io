---
id: 78
title: Mac OS X ServerでMacPortsを共有
date: 2010-12-28T12:11:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2010/12/28/mac-os-x-server%e3%81%a7macports%e3%82%92%e5%85%b1%e6%9c%89/'
permalink: /2010/12/28/mac-os-x-servermacports-sharing/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2010/12/mac-os-x-servermacports.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/5050530502190804611
categories:
  - コンピュータ
tags:
  - Mac OS X Server
  - macports
---
MacPortsを使うと，フリーウェアのインストール手間が大幅に軽減される．しかし台数が増えてくると，アップデートも手間に感じられるようになってくる．そこでMacPortsを共有することを考えた．

MacPortsのインストールされたXserveで/optを共有しようとしたら，サーバ管理の共有には表示されなかった．表示されないディレクトリに移動するときは，Finderで移動&gt;サーバに接続...を選ぶところだ．サーバ管理には隠しディレクトリを表示するオプションは見当たらない．アップルの<a href="http://support.apple.com/kb/HT3116?viewlocale=ja_JP&amp;locale=ja_JP">記事</a>によると，コマンドラインを使う必要があることが分かった．

以下を実行すると共有ポイントとして表示される．/optが格納されているボリューム（たとえばServer HD）には表示されない．
<pre>
sudo sharing -a /opt</pre>
AFPで思ったところ（/opt/local）にマウントできなかったので，上記の方法は中止．

昔ながらのNFSでエクスポートとマウントすることにした．
<ol>
 	<li>サーバ側で/etc/exportsに記述.</li>
 	<li>NFSを起動 (sudo nfsd enable).</li>
 	<li>クライアント側でマウント (sudo mount_nfs サーバ:/opt/local マウントポイント)</li>
 	<li>クライアント側で/etc/fstabに記述.</li>
</ol>