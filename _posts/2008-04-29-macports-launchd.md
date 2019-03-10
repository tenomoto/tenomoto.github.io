---
id: 181
title: MacPortsとlaunchd
date: 2008-04-29T11:14:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2008/04/29/macports%e3%81%a8launchd/'
permalink: /2008/04/29/macports-launchd/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2008/04/macportslaunchd.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/5787622348620554950
categories:
  - コンピュータ
tags:
  - launchd
  - Mac
  - macports
---
Mac OS Xのデーモン管理は、10.4からlaunchdが導入された。10.5からはStartupItemsが廃止されて、launchdだけとなった。ユーザレベルでも使える反面、XML形式のplistを作成する必要があり面倒になった面もある。

MacPortsでは、パッケージ作成者にもユーザにも使いやすい仕組みが提供されている。詳細は<a href="http://guide.macports.org/#reference.startupitems">MacPorts Guide</a>参照。

パッケージ作成者は、startupitem.*に起動スクリプトやログの保存場所等の情報を属性として記述すれば、/opt/local/etc/LaunchDaemonsにplistが作成され、/Library/LaunchDaemonsにシンボリックリンクが張られる。既定では、デーモンは「起動しない」というラベルがついている。

ユーザは、
<pre>sudo launchctl load -w /Library/LaunchDaemons/org.macports.パッケージ名.plist</pre>
を実行すればデーモンを起動できる。再び起動しないようにするには、サブコマンドloadの代わりにunloadを使う。