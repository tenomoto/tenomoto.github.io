---
id: 75
title: lsbomでreceiptの中身を調べる
date: 2011-01-18T12:17:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2011/01/18/lsbom%e3%81%a7receipt%e3%81%ae%e4%b8%ad%e8%ba%ab%e3%82%92%e8%aa%bf%e3%81%b9%e3%82%8b/'
permalink: /2011/01/18/lsbom-receipt/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2011/01/lsbomreceipt.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/8729629277620833098
categories:
  - コンピュータ
tags:
  - lsbom
  - Mac
---
MacPorts-develでMac OS X 10.6.6で多数の/usrのファイルが追加または更新されたことが話題になった．更新されたファイルの確認は，lsbomでできる．忘れそうなのでメモ．
<pre>
$ lsbom /var/db/receipts/com.apple.pkg.update.os.10.6.6.patch.bom | grep /usr</pre>