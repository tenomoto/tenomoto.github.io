---
id: 222
title: g95のMacPotsパッケージ
date: 2007-03-03T13:28:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2007/03/03/g95%e3%81%aemacpots%e3%83%91%e3%83%83%e3%82%b1%e3%83%bc%e3%82%b8/'
permalink: /2007/03/03/g95-macpots-package/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2007/03/g95macpots.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/6601028270476952709
categories:
  - コンピュータ
tags:
  - Fortran
  - g95
  - macports
---
Whitakerさんが書いたFinkの.infoを参考にして, g95のportを書くことができた．

odcctoolsもバージョンを20060608に合わせた．このようにして作ったg95-0.90だと-read_only_relocsを使う必要 がないようだ．netcdf, libnc-dap, octaveのportを書き直した．*.tgzはローカルのdportsの中で展開する．カテゴリ/パッケージ名/Portileという構 成．netcdf, libnc-dap, octaveでは，g95はvariantsのひとつであるので，+g95をつけてport installする．以下の順序でインストールするとよいだろう．