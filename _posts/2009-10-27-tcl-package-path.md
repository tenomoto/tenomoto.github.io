---
id: 106
title: Tclパッケージのパス
date: 2009-10-27T12:28:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2009/10/27/tcl%e3%83%91%e3%83%83%e3%82%b1%e3%83%bc%e3%82%b8%e3%81%ae%e3%83%91%e3%82%b9/'
permalink: /2009/10/27/tcl-package-path/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2009/10/tcl.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/7250515234643590584
categories:
  - コンピュータ
tags:
  - macports
  - Tcl
---
Mac OS X添付の/usr/bin/tclshは, ~/Library/Tclにパッケージをおけば見つけてくれる.
MacPortsでインストールした/opt/local/bin/tclshは,
<pre>
$ /opt/local/bin/tclsh
% set auto_path
/opt/local/lib/tcl8.5 /opt/local/lib</pre>
しか見ていない.

環境変数TCLLIBPATHに追加するか，スクリプトの冒頭で
<pre>
lappend auto_path /Users/foo/Library/Tcl</pre>
と書けば追加できる. Tclで完結する後者の方が良さそう.