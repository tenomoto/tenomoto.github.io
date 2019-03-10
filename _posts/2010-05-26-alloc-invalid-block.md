---
id: 94
title: 'alloc: invalid block'
date: 2010-05-26T11:25:00+09:00
author: takeshi
layout: post
guid: https://www.enomosphere.net/2010/05/26/alloc-invalid-block/
permalink: /2010/05/26/alloc-invalid-block/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2010/05/alloc-invalid-block.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/3638082302486447482
categories:
  - コンピュータ
tags:
  - macports
  - Tcl
---
Tigerで更新したportsのチェックをしようとしたところ，<br /><pre>alloc: invalid block</pre><br />というエラーが出た．Tclから出ているらしい．<br /><pre>export MACOS_DEPLOYMENT_TARGET=10.4</pre><br />としたらエラーは出なくなった.<br /><br />しかしコンパイル時にバスエラーが出る．<br />TigerはもうMacPortsではサポートしていないが，明らかに何かおかしい．