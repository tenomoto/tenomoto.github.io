---
id: 173
title: プリンタ共有
date: 2008-08-19T12:53:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2008/08/19/%e3%83%97%e3%83%aa%e3%83%b3%e3%82%bf%e5%85%b1%e6%9c%89/'
permalink: /2008/08/19/printer-sharing/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2008/08/blog-post_19.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/7916426376425055859
categories:
  - コンピュータ
tags:
  - Linux
  - Mac
  - Ubuntu
  - Windows
---
<div>

Mac mini (PPC, Mac OS X 10.4)につないでいるCanon MP810をWindowsやLinuxからも使えるようにした。

いままではほかのMacから同じプリンタを共有していた。Windows共有をOnにすればプリンタも自動的に共有できるのかと思っていたのだが、<a href="http://www7a.biglobe.ne.jp/~tzwada/Mac/printer/index.html">ここ</a>によると/etc/cups/printers.confの編集が必要だと分かった。

Ubuntuからのプリントにも成功した。キヤノンからLinux用のドライバが出ているが、lienを使ったrpmでdebへの変換に失敗した。 amd64では簡単では無いようだ。だめもとでプリンタを追加して、OpenPrinting databaseにある情報を参考にしてip4200を選んだところ印刷できた。

</div>