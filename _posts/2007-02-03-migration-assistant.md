---
id: 224
title: 移行アシスタント
date: 2007-02-03T13:58:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2007/02/03/%e7%a7%bb%e8%a1%8c%e3%82%a2%e3%82%b7%e3%82%b9%e3%82%bf%e3%83%b3%e3%83%88/'
permalink: /2007/02/03/migration-assistant/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2007/02/blog-post_03.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/8440080141003597585
categories:
  - コンピュータ
tags:
  - Mac
---
Mac OS Xをクリーンインストールしたときや、新しいマシンに電源を入れたときに起動する移行アシスタントは、大変便利だ。

アプリケーション、ネットワークの設定、ユーザファイルを新しい環境にコピーしてくれる。ネットワークにもつながるし、アプケーションもインストール済な ので、すぐにでも使い始めることができる。FinkやDarwinPortsも移行してくれる。ただし、/usr/X11や/usr/localは移行し てくれない。X11は再インストールする。/usr/localは必ずコピーすることと覚えてもよいが、これからはFinkの/sw、 DarwinPortsの/optと同様に/localにして、/usrにはシンボリックリンクをはっておくことにした。サーバをやっている場合は、 /etc/hostconfig, /etc/hosts, /etc/httpd/httpd.confなども手動で設定し直す必要がある。