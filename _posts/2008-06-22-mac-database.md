---
id: 177
title: Macでデータベースを使う
date: 2008-06-22T11:58:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2008/06/22/mac%e3%81%a7%e3%83%87%e3%83%bc%e3%82%bf%e3%83%99%e3%83%bc%e3%82%b9%e3%82%92%e4%bd%bf%e3%81%86/'
permalink: /2008/06/22/mac-database/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2008/06/mac.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/3362921390889354945
categories:
  - コンピュータ
tags:
  - Mac
  - SQLite
---
OSの検索機能やインターネット検索エンジンが良くなったので、適当に保存して検索すれば足りることも多いが、データベースに整理しておきたいものもある。

Mac OSの時代は、クラリスワークスにデータベースがついていたし、HyperCardもあった。ファイルメーカーは今も健在で、お手軽なBentoも発売された。AddressBook、Safariのブックマーク、論文リストを扱える<a href="http://bibdesk.sourceforge.net/">BibDesk</a>など専用のアプリケーションもある。Mailは多くの人にとって最も重要なデータベースかもしれない。

一方、Mac OS Xになって、フリーのリレーショナルデータベースシステム (RDBMS) が使えるようになった。MySQLなどクライアントサーバ型のRDBMSは、Webアプリケーションを使うときに導入する程度で、自分で使いこなすには敷居が高い。

<a href="http://www.sqlite.org/">SQLite</a>はクライアントサーバ型でない、スタンドアローンのRDBMSである。コマンドラインやC言語、Tclのインターフェースが提供されている。文字列は、UTF-8なので日本語も問題なく格納できる。Tclの文字列もUTF-8なので、Tclから使えば文字化けの問題はない。

簡単な使い方は、<a href="http://www.sqlite.org/quickstart.html">quickstart</a>に紹介されている。Mac OS X Leopard添付のSQLite3/Tclでは、共有ライブラリの名前とパスが異なる。新たに文献リストを作り、1レコード追加して表示するTclスクリプトは次の通り。
<pre>load /usr/lib/sqlite3/libtclsqlite3.dylib Sqlite3
sqlite3 db "test.db"
db eval {create table mypapers(id integer primary key, authors, year, title, journal, issue, pages)}
db eval {insert into mypapers values(NULL, 'Me', 2008, 'How to use sqlite3 on Mac', 'unknown', '1', '1--99')}
puts stdout [db eval {select * from mypapers}]
db close</pre>
コマンドはsqlite3のひとつだけ。sqlite3の次がTclの中でデータベースを差すもので、新たなコマンドとなる。2つ目の引数はファイル名。既にファイルがあれば開かれ、なければ新しいファイルが作られる。evalのあとにSQL文を書く。最後はデータベースを閉じている。