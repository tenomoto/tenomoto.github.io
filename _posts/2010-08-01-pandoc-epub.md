---
id: 89
title: pandocでepub
date: 2010-08-01T16:35:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2010/08/01/pandoc%e3%81%a7epub/'
permalink: /2010/08/01/pandoc-epub/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2010/08/pandocepub.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/4197541722508224952
categories:
  - コンピュータ
tags:
  - epub
  - Haskell
  - pandoc
---
さまざまな形式の文書が作成できる<a href="http://johnmacfarlane.net/pandoc/index.html">pandoc</a>が1.6から<a href="http://johnmacfarlane.net/pandoc/epub.html">epubに対応</a>.

残念ながらMacPortsのpandocは古く, ビルドにも問題があるようだ

pandocは<a href="http://hackage.haskell.org/platform/">Haskell</a>で書かれている. Haskellは, コンパイラghcだけでなく, 独自のパッケージ管理システムcabal等を含む包括的なプラットフォーム

まず, Mac OS X用のHaskellをインストール
ghcは/usr/bin, cabalは/usr/localにインストールされる

次にpandocのインストール
<pre>cabal updat
cabal install pandoc</pre>

バイナリは~/.cabal/binに, マニュアルは~/.cabal/share/manにインストールされる

MacPortsのptexにはunicodeパッケージは含まれないので，別途入手し~/texmf/texなどに置く（置いたらmktexlsr）．

Mac上では<a href="http://www.adobe.com/jp/products/digitaleditions/">Adobe Digital Editions</a>でepub形式のファイルを読むことができ