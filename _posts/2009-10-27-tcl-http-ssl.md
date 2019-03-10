---
id: 107
title: Tcl httpでssl
date: 2009-10-27T12:14:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2009/10/27/tcl-http%e3%81%a7ssl/'
permalink: /2009/10/27/tcl-http-ssl/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2009/10/tcl-httpssl.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/8267781571216879011
categories:
  - コンピュータ
tags:
  - Tcl
---
SSLでログインしたあと, ファイルをダウンロードするためのTclスクリプトを書いてみる. wgetやcurlを使ってもよいが, tlsパッケージを併用するとhttpでSSL (https) が扱える.

<pre>
package require http
package require tls
::http::register https 443 ::tls::socket</pre>
SSLサイトでのログイン. まず::http::formatQueryでPOSTするデータを作る. 送信すべきデータはサイトにより異なる.
<pre>
set login [::http::formatQuery email $email passwd $passwd action login]</pre>
メタデータからクッキーをリストに保存.
<pre>
set tok [::http::geturl $loginurl -query $login]
upvar #0 $tok state
set cookies [list]
foreach {name value} $state(meta) {
if {$name eq "Set-Cookie"} {
  lappend cookies [lindex [split $value {;}] 0]
}
}
::http::cleanup $tok</pre>
クッキーは, ヘッダにつけて送信.
<pre>
set tok2 [::http::geturl $dataurl$fname -headers [list Cookie [join $cookies {;}]]]</pre>
リダイレクトされる場合は, メタデータのLocationを使う.
<pre>
upvar #0 $tok2 state
array set meta $state(meta)</pre>
$meta(Location)にURLが入っているはず.
リダイレクト先からのダウンロードにもクッキーが必要.
<pre>
set tok3 [::http::geturl $meta(Location) -channel $f -headers [list Cookie [join $cookies {;}]]]
::http::cleanup $tok2
::http::cleanup $tok3</pre>