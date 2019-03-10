---
id: 111
title: MacPortsでphp5をインストール
date: 2009-10-03T18:16:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2009/10/03/macports%e3%81%a7php5%e3%82%92%e3%82%a4%e3%83%b3%e3%82%b9%e3%83%88%e3%83%bc%e3%83%ab/'
permalink: /2009/10/03/macports-php5/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2009/10/macportsphp5.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/4664430934607888233
categories:
  - コンピュータ
tags:
  - Mac
  - macports
  - PHP
---
Snow LeopardのPHP5はGDが有効化されているが，freetypeがサボートされていない．そこでMacPortsからインストール
MacPortsの<a href="http://trac.macports.org/wiki/howto/MAMP">HowTo</a>も参考に．
<pre>
$ sudo port -d install php5 +pear
$ sudo port -d install php5-mysql
$ sudo port -d install php5-gd</pre>
標準のapache2にphp5のモジュールをロードするために，/etc/apache2/httpd.confを編集.
<pre>
LoadModule php5_module /opt/local/apache2/modules/libphp5.so</pre>
MySQL5との接続.
<pre>
$ cd /opt/local/etc/php5/
$ sudo cp php.ini-development php.ini</pre>
MySQL5に接続するために，php.iniを編集
<pre>
pdo_mysql.default_socket= /opt/local/var/run/mysql5/mysqld.sock
mysql.default_socket = /opt/local/var/run/mysql5/mysqld.sock
mysqli.default_socket = /opt/local/var/run/mysql5/mysqld.sock</pre>
Apache2を再起動．
<pre>
$ sudo apachectl graceful</pre>