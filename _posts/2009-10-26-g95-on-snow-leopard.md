---
id: 109
title: g95 on Snow Leopard
date: 2009-10-26T21:41:00+09:00
author: takeshi
layout: post
guid: https://www.enomosphere.net/2009/10/26/g95-on-snow-leopard/
permalink: /2009/10/26/g95-on-snow-leopard/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2009/10/g95-on-snow-leopard.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/8781481557455004981
categories:
  - コンピュータ
tags:
  - g95
  - macports
  - Snow Leopard
---
Snow Leopardでg95がコンパイルできずに苦労している．

gcc-4.0.4はi386では一応コンパイルできるが, g95のコンパイル途中で失敗する．

gcc-4.0.4とgcc-4.1.2では, configureで--buildにx86_64-apple-darwin10を与えるとうまくいかない．<br />x86_64はサポートされていないようだ．

Appleが修正したgcc-5465は，i386とx86_64両方のライブラリを作る．g95のコンパイルのときに，未定義のシンボルが多数出てしまいどうしようもなくなった．

gcc-4.3.4はいろいろと細工をして最後までコンパイルすることはできたが，g95の実行時にエラーが出る．gcc-4.3では，仕組みが大きく変わったのだろう．そこまで直せそうにない．

それならばとgcc-4.2.4を試したみた．gcc-4.3.4でしたような細工がいくつか必要だったが，gcc-4.3.4よりは難しくなかった．一応コンパイルに成功し，簡単なプログラムが動作することを確認した．細工にはいい加減なものもあるので，あとで問題が発生するかもしれない．それでもともかくめでたい．fileで確認したところ，確かにx86_64のコードが生成されている．

次はこれをPortfileにまとめなくてはならない．

11/9追記: gcc-4.2.4にリンクしたg95は, Snow LeopardだけでなくIntel MacであればTigerでもLeopardでも動いたが, PowerPCのMacでは動かなかった. そこで, 従来の4.0.4をベースにしてgcc42はvariantととした. <a href="http://trac.macports.org/changeset/60290">r60290</a>で変更をコミットした.<br />さらに<a href="http://trac.macports.org/changeset/60340">r60340</a>でSnow Leopardの検出を簡素化した.