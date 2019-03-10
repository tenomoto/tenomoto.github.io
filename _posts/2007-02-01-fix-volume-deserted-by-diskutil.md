---
id: 225
title: ディスクユーティリティに見放されたら…
date: 2007-02-01T16:01:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2007/02/01/%e3%83%87%e3%82%a3%e3%82%b9%e3%82%af%e3%83%a6%e3%83%bc%e3%83%86%e3%82%a3%e3%83%aa%e3%83%86%e3%82%a3%e3%81%ab%e8%a6%8b%e6%94%be%e3%81%95%e3%82%8c%e3%81%9f%e3%82%89/'
permalink: /2007/02/01/fix-volume-deserted-by-diskutil/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2007/02/blog-post_01.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/6269330033848364963
categories:
  - コンピュータ
tags:
  - Mac
---
<div>

ボリューム名を見つけて
<pre>fsck_hfs -r ボリューム名</pre>
を試してみよう．ディスクに連続した空き領域があるなど一定の条件を満たすときに，カタログファイルを再構築できることもある.

なお，ディスクユーティリティで，ディスクの修復は，
<pre>diskutil repairvolume ボリューム名</pre>
に対応していると思われる．

</div>