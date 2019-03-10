---
id: 112
title: MacPortsでmysql5をインストール
date: 2009-09-25T23:48:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2009/09/25/macports%e3%81%a7mysql5%e3%82%92%e3%82%a4%e3%83%b3%e3%82%b9%e3%83%88%e3%83%bc%e3%83%ab/'
permalink: /2009/09/25/macports-mysql5/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2009/09/macportsmysql5.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/2730469556663888675
categories:
  - コンピュータ
tags:
  - macports
  - MySQL
---
<div>mysql5のインストール</div>
&nbsp;
<pre>sudo port install mysql5</pre>
サーバとして使うにはmysql5-serverもインストールする.
<div>
<div>データベース格納用ディレクトリの作成</div>
<pre>sudo mkdir -p /opt/local/var/db/mysql5
sudo chown mysql /opt/local/var/db/mysql5</pre>
<div>プロセスIDファイル用ディレクトリの作成</div>
<pre>sudo mkdir -p /opt/local/var/run/mysql5
sudo chown mysql /opt/local/var/run/mysql5</pre>
<div>初期化</div>
<pre>sudo -u mysql mysql_install_db5</pre>
<div>起動</div>
<pre>sudo /opt/local/share/mysql5/mysql/mysql.server start</pre>
<div>起動の確認</div>
<pre>mysql5 -u root</pre>
<div>パスワード変更</div>
<pre>/opt/local/lib/mysql5/bin/mysqladmin -u root password 'password'</pre>
</div>