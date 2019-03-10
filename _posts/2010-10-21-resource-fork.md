---
id: 84
title: リソースフォーク
date: 2010-10-21T17:00:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2010/10/21/%e3%83%aa%e3%82%bd%e3%83%bc%e3%82%b9%e3%83%95%e3%82%a9%e3%83%bc%e3%82%af/'
permalink: /2010/10/21/resource-fork/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2010/10/blog-post.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/4655977801568393611
categories:
  - コンピュータ
tags:
  - Mac
---
Safariでデータをダウンロードしたら，リソースフォークがついてしまった．tarしたときに気がついた．過去の遺産, そろそろ廃止してほしい.

tarするときは分離されるが, ゴミが含まれてしまう.
環境変数を設定すると, データだけがアーカイブされる.
<pre>
export COPYFILE_DISABLE=true</pre>
<a href="http://macwiki.sourceforge.jp/wiki/index.php/%E3%83%AA%E3%82%BD%E3%83%BC%E3%82%B9%E3%83%95%E3%82%A9%E3%83%BC%E3%82%AF">MacWiki: リソースフォーク</a>