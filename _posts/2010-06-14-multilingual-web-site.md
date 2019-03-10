---
id: 90
title: 多言語ウェブサイト
date: 2010-06-14T16:15:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2010/06/14/%e5%a4%9a%e8%a8%80%e8%aa%9e%e3%82%a6%e3%82%a7%e3%83%96%e3%82%b5%e3%82%a4%e3%83%88/'
permalink: /2010/06/14/multilingual-web-site/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2010/06/web.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/2581765549655110150
categories:
  - コンピュータ
tags:
  - Apache
  - Mac
---
同僚に教えてもらったことを糸口に, ウェブサイトの日本語と英語となど言語の切り替えについて調べた．

言語やエンコーディングなどの処理は, mod_mimeが担当. 言語, 文字セットと拡張子との対応は, MacのApache2の場合/etc/httpd/extra/httpd-languages.confに定義されていて，特に設定の必要はない. もしhttpd.confで読み込みがコメントアウトされている場合は, コメントアウトを外す. またOptionsにMultiviewsが必要なのでうまくいかないときは確認する.

順序は何でもよさそうなのだが, MacのApache2では, ja.htmlではうまくいかずhtml.jaだとうまくいった

Safariの場合, ブラウザ自体の言語設定はなく, システム環境設定の「言語とテキスト」で設定. Safariを再起動すると有効になる.

2013/04/01追記

DirectoryIndexをindexとするとhtml.jaでもうまくいく．DirectoryIndexがindex.htmlだとindex.html.en, index.html.fr, index.html.jaから選ばれ，index.ja.htmlは対象にならないためうまくいかなかった．

2013/04/02追記

Lion Serverは複数のサイトをホストできるようになっている．デフォルトのサイトの設定ファイルは/etc/apache2/sites/0000_any_80_.confで，こちらにDirectoryIndexが指定されているので，ここを直さないと403 (Forbidden) エラーが発生する．