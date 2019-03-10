---
id: 51
title: Mountain LionでMacPorts
date: 2012-07-29T11:39:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2012/07/29/mountain-lion%e3%81%a7macports/'
permalink: /2012/07/29/mountain-lion-macports/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2012/07/mountain-lionmacports.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/8167165068871202656
categories:
  - コンピュータ
tags:
  - Mac
  - macports
---
AppStoreからXcode 4.4をダウンロード．<!--more-->

Xcodeを起動．Xcode &gt; Preferences &gt; DownloadsでCommand Line Toolsをインストール．
Xcodeのライセンスを確認．
<pre>$ sudo xcodebuild -license</pre>
<pre></pre>
<a href="http://xquartz.macosforge.org/">Xquartz</a>をインストール． MacPorts-2.1.2を<a href="http://trac.macports.org/wiki/InstallingMacPorts">インストール</a>． インストールしてある場合は更新．
<pre></pre>
<pre>$ sudo port -d selfupdate</pre>
OSが更新されたら，<a href="http://trac.macports.org/wiki/Migration">全て入れ直す</a>．
<pre></pre>
<pre>port -qv installed &gt; myports.txt
$ sudo port -f uninstall installed
$ sudo port clean all</pre>
myports.txtを見ながらパッケージを再インストール．7/29現在Mountain Lion用のバイナリがないので，ソースからコンパイルされる．