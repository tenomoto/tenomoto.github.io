---
id: 229
title: 電脳Ruby on Mac OS X
date: 2006-12-31T16:53:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2006/12/31/%e9%9b%bb%e8%84%b3ruby-on-mac-os-x/'
permalink: /2006/12/31/dcl-ruby-on-mac-os-x/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2006/12/ruby-on-mac-os-x.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/5562748285665479380
categories:
  - コンピュータ
tags:
  - DCL
  - Mac
  - Ruby
---
<div>

電脳RubyをMac OS Xにインストールしてみました．どなたか熱心な方，FinkのパッケージかDarwinPortsのportsを書いてください．

# 東大の岩前さんによる<a href="http://www.gfd-dennou.org/arch/cc-env/fink-dennou/">Finkパッケージ</a>
<h4>インストール</h4>
電脳Rubyで提供されている一括インストーラは，基本的にはMacでも動くが，/usr/localなど管理者権限が必要なところにインストール するときはsudoをつける必要がある．ダウンロードしたファイルや展開したソースがすべて管理者の所有になってしまう．時々FTPサイトからリストをと れないことがあるようだ．一括インストーラと手動インストールを併用してgaveまでインストールすることができた．以下，手動でインストールしたものだ けまとめておく．
<h5>ソースの入手先</h5>
<ul>
 	<li><a href="http://www.ruby-lang.org/">Ruby</a></li>
 	<li><a href="http://www.ir.isas.ac.jp/~masa/ruby/">NArray</a></li>
 	<li><a href="http://www.gfd-dennou.org/arch/ruby/index-j.htm">電脳Ruby</a></li>
</ul>
<h5>ruby-1.8.4</h5>
Mac OS X 10.4にプレインストールされているものより新しいし，/usr/libはいじりたくないので，新たに/usr/localに入れることにした．make; make installで問題なくインストールできた．
<h5>dcl-5.3.1-C</h5>
GTK+2.0はFinkからインストール．ソースの改変が<a href="http://www-clim.kugi.kyoto-u.ac.jp/satomura/memo/comp_memo/DCLonMac.html">必要</a>なので，手動でインストール．src/grph1/swpack/zxpack.cのwaitが/usr/include/sys/wait.hの定義とぶつかるので，別の名前にする．
<h5>ruby-dcl-1.5.2</h5>
NArray, NArrayMissは一括インストーラを使ってインストールした．lib/dcl.rbの冒頭にrequire “gtk2″と<a href="http://www-aos.eps.s.u-tokyo.ac.jp/pukiwiki/pukiwiki.php?MacOSX%2FDCLBuildMemo">書く</a>．ruby extconf.rb; make; make installでインストールできる．

</div>