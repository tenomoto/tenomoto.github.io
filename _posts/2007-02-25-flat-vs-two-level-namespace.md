---
id: 223
title: 名前空間
date: 2007-02-25T14:17:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2007/02/25/%e5%90%8d%e5%89%8d%e7%a9%ba%e9%96%93/'
permalink: /2007/02/25/flat-vs-two-level-namespace/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2007/02/blog-post.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/7271445111462525938
categories:
  - コンピュータ
tags:
  - Mac
  - name space
---
Mac OS Xで動的リンクを使うときは, -flat_namespace -undefined suppressにするものと思っていたが, 最近は違うようだ. Panther以降は, 環境変数MACOSX_DEPLOYMENT_TARGET=10.4 (10.3以降にする) として, two-level名前空間のまま, -undefined dynamic_lookupとするのがよいようだ.