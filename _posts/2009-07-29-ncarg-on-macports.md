---
id: 121
title: ncarg on MacPorts
date: 2009-07-29T22:45:00+09:00
author: takeshi
layout: post
guid: https://www.enomosphere.net/2009/07/29/ncarg-on-macports/
permalink: /2009/07/29/ncarg-on-macports/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2009/07/ncarg-on-macports.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/2185883991702369318
categories:
  - コンピュータ
tags:
  - macports
  - NCL
---
<a href="http://www.ncl.ucar.edu/">ncl</a>のソースが公開されて随分経つが, ソースのコンパイルは先延ばしにしてきた. ついに, Portfileを作成してコミットした. 

ビルドシステムは, configureやCMakeではなく, 独自cshスクリプトとymakeだが案外順調に進んだ.

HDFのヘッダをhdf/mfhdf.hで参照しているので, hdf/を削除するというパッチは必要だった. g2clibはwgrib2のものを使った. hdfeosにはPortfileを書いた. gcc43が既定のfortranコンパイラとなったが, +g95でg95でもコンパイルできる.

BLASのコンパイルに時間をかけているが, Macにはaccelerateフレームワークがあるから無駄なような気がする. でも, 最初は安全重視でncarg添付のものを使った.