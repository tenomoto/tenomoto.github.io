---
id: 114
title: gnudatalanguage +universal
date: 2009-08-14T15:21:00+09:00
author: takeshi
layout: post
guid: https://www.enomosphere.net/2009/08/14/gnudatalanguage-universal/
permalink: /2009/08/14/gnudatalanguage-universal/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2009/08/gnudatalanguage-universal.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/8190186437506497279
categories:
  - コンピュータ
tags:
  - GDL
  - macports
---
gnudatalanguageのPortfileには問題はないが, +universalが失敗することがある.<div><br /></div><div>これは, python25+universalがuniversalとは言っても, i386とppcの2種類のアーキテクチャ用のバイナリをつくるため (<a href="http://trac.macports.org/ticket/17501">r17501</a>). Intel Macでsources.confのuniversal_archsにx86_64が入っていてもi386とppc用に作られてしまう.</div>