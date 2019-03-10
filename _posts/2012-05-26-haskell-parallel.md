---
id: 54
title: Haskellで並列プログラミング
date: 2012-05-26T09:15:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2012/05/26/haskell%e3%81%a7%e4%b8%a6%e5%88%97%e3%83%97%e3%83%ad%e3%82%b0%e3%83%a9%e3%83%9f%e3%83%b3%e3%82%b0/'
permalink: /2012/05/26/haskell-parallel/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2012/05/haskell.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/5035923104006475375
categories:
  - コンピュータ
tags:
  - Haskell
  - Lion
---
2012年5月に<a href="http://hackage.haskell.org/platform/">Haskell Platform</a>の新しいバージョンが出るようなので，待った方がよいかも．→出ました．<!--more-->

<a href="http://www.haskell.org/haskellwiki/Haskell%E5%85%A5%E9%96%80_5%E3%82%B9%E3%83%86%E3%83%83%E3%83%97">Haskell入門5ステップ</a>の4.1 初めてのHaskell並列プログラミングでつまづいた．
<pre>Most RTS options are disabled</pre>
-rtsoptsをつけてもエラーが出続ける. 以下の通り, 最新GHCとcabal-installを入れたところうまくいった．
<ol>
 	<li><a href="http://www.haskell.org/ghc/download_ghc_7_4_1">ghc-7.4.1</a>をインストール．</li>
 	<li>cabal-install
<pre>$ git clone git://github.com/ibtaylor/cabal-install.git
$ cd cabal-install
$ sudo bash -c 'unset PATH; . /etc/profile; bash bootstrap.sh --global'</pre>
</li>
 	<li>パッケージ情報の更新.
<pre>$ cabal update</pre>
</li>
 	<li>parallelパッケージのインストール.
<pre>$cabal install parallel</pre>
</li>
</ol>