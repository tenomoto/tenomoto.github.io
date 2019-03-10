---
id: 147
title: plplot-5.9.2 revision 1
date: 2009-02-22T19:06:00+09:00
author: takeshi
layout: post
guid: https://www.enomosphere.net/2009/02/22/plplot-5-9-2-revision-1/
permalink: /2009/02/22/plplot-5-9-2-revision-1/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2009/02/plplot-592-revision-1.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/356203480584022639
categories:
  - コンピュータ
tags:
  - dlang
  - PLplot
---
D言語のbindingとcairo/pangoドライバをvariantsとして追加．cairoドライバによりPDFが作成できるようになる．g95, gdc, cairoを有効にしてインストールするには，<br /><pre>sudo port -d install plplot +g95 +gdc +cairo<br /></pre>とする．<br /><br />D言語サンプルは，bindingがexperimentalなので少ないが，/opt/local/share/plplot-5.9.2/examples/dにいくつかある．コンパイルは，ヘッダ/opt/local/include/plplot/plplot.d，モジュール本体は/opt/local/lib/libplplotd.dylibなので，<br /><pre>gdmd -I/opt/local/include/plplot x03d.d /opt/local/lib/libplplotd.dylib</pre>とする．gdcでなくgdmdを使うとソースコードから.dをとった名前のバイナリができる．簡単なプログラムでは便利．-lオプションはないようだ．