---
id: 113
title: Snow LeopardとMacPorts 1.8
date: 2009-08-29T19:48:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2009/08/29/snow-leopard%e3%81%a8macports-1-8/'
permalink: /2009/08/29/snow-leopard-macports-1-8/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2009/08/snow-leopardmacports-18.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/654640180194759559
categories:
  - コンピュータ
tags:
  - Mac
  - macports
---
Snow Leopardを上書きインストールすると, 一見/optが消去されたように見える. ディスクの空き領域も増えている. 実は, /optはFinderで見えなくなっているだけで, 消去されていない. ディスクに余裕ができたのは, システムのPowerPC用の部分がSnow Leopardではなくなったから.
<div></div>
<div>ただし, Snow Leopardと相前後してリリースされたMacPorts 1.8は以前のバージョンと仕様が変わり, デフォルトではCPUに応じたアーキテクチャが選択される. 例えば, Core 2 Duoを使ったMacBook ProやXeonを搭載したMac Proなら, 既定ではx86_64用にコンパイルされる. 1.7以前はi386用にコンパイルされていた. そのため, この例の場合, これまでのものを引き継ぐとアーキテクチャの違いから, リンクがうまくいかなくなる.</div>
<div></div>
<div>64-bit CPUを搭載したマシンで64-bitのコード生成は, 科学技術計算にはメリットがあるので, 歓迎すべき仕様変更である. 手間となるが, コンパイルしなおすのがよさそうだ. Leopardでコンパイルしたものは32-bitだが, ディレクトリの名前を変更すれば使い続けることができる (例えば/opt/localを/opt/local_i386).</div>
<div></div>
<div>MacPortsはボランティアにより支えられているので, 一朝一夕にすべてが移行できるわけではなく, 中にはSnow Leopardでうまくコンパイルできなくなるものもある. しばらく時間がかかるかもしれないが, 徐々に移行されていくはずだ. MacPortsは現行OSとその前までをサボートするので, Tigerはlegacyとなり積極的なサポートはなくなる. TigerユーザはLeopard, Snow Leopardへの移行を迫られるか, コンパイルできなくなるパッケージが出てくるという心づもりが必要だ.</div>
<div></div>
<div>Snow Leopardでは, XCode 3.2となった. XCode 3.2は, Snow LeopardのDVDのOptional Installsにある. デフォルトのコンパイラは, gcc-4.2となったようである.</div>