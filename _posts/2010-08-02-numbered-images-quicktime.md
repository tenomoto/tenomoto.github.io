---
id: 88
title: 連番画像をQuickTimeに
date: 2010-08-02T14:23:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2010/08/02/%e9%80%a3%e7%95%aa%e7%94%bb%e5%83%8f%e3%82%92quicktime%e3%81%ab/'
permalink: /2010/08/02/numbered-images-quicktime/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2010/08/quicktime.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/274504499179099124
categories:
  - コンピュータ
tags:
  - Mac
  - QuickTime
---
<a href="http://macwiki.sourceforge.jp/wiki/index.php/QuickTime#AppleScript">MacWiki</a>にあるものを少し修正. Snow LeopardではQuicktime PlayerではなくQuickTime Player 7とする.
<pre>tell application "QuickTime Player"
 activate
 set firstFile to choose file with prompt "連番の最初のファイルを選択"
 display dialog "1秒あたりのフレーム数" buttons {"OK"} default answer "2" default button 1 with icon 1
 -- open image sequence firstFile seconds per frame 2
 open image sequence firstFile frames per second text returned of result
 save document 1 as self contained
end tell</pre>
2011/1/17追記. Snow Leopardでは上記スクリプトはコンパイルできず．Leopardで書いたスクリプトをSnow Leopardで開いたら，以下のようになっていた．
<pre>tell application "QuickTime Player"
 activate
 set firstFile to choose file with prompt "連番の最初のファイルを選択"
 display dialog "1秒あたりのフレーム数" buttons {"OK"} default answer "2" default button 1 with icon 1
 -- open image sequence firstFile seconds per frame 2
 «event MVWRopis» firstFile given «class fpsc»:text returned of result
 save document 1 as «constant savkflat»
end tell</pre>