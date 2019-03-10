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
<!--more-->

## mysql5のインストール

<pre>sudo port install mysql5</pre>
サーバとして使うにはmysql5-serverもインストールする.

## データベース格納用ディレクトリの作成

<pre>sudo mkdir -p /opt/local/var/db/mysql5
sudo chown mysql /opt/local/var/db/mysql5</pre>

## プロセスIDファイル用ディレクトリの作成

<pre>sudo mkdir -p /opt/local/var/run/mysql5
sudo chown mysql /opt/local/var/run/mysql5</pre>

## 初期化
<pre>sudo -u mysql mysql_install_db5</pre>
<div>起動</div>
<pre>sudo /opt/local/share/mysql5/mysql/mysql.server start</pre>

## 起動の確認

<pre>mysql5 -u root</pre>

## パスワード変更

<pre>/opt/local/lib/mysql5/bin/mysqladmin -u root password 'password'</pre>

