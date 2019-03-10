---
id: 165
title: DiskWarrior
date: 2008-11-12T18:25:00+09:00
author: takeshi
layout: post
guid: https://www.enomosphere.net/2008/11/12/diskwarrior/
permalink: /2008/11/12/diskwarrior/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2008/11/diskwarrior.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/4398227657597921566
categories:
  - コンピュータ
tags:
  - DiskWarrior
  - Mac
---
LaCieの外付けHDD 1.5TBの調子が悪くなった．昨日は虹色カーソルになることが多かったので，本体の調子が悪いのかと誤解していた．このディスクには，論文やスライド等重要なデータが保存されていた．もともと地形や海面水温，再解析等のデータ用だったが，内蔵が手狭になりこちらを使っていた．重要なファイルがあるのに，このHDDをTime Machineとしても使っており，最近のバックアップはなかった．そのうち整理しようと思っていたが，手遅れだった．ディレクトリが破損しており，fsck_hfsは失敗した．幸いマウントしたので，この2年間の論文やスライドをバックアップした．

あとは初期化しても良かったのだか，データをまた集め直すのは大変なので，<a href="http://www.amazon.co.jp/gp/product/B000LPS54C?ie=UTF8&amp;tag=enomospheddoj-22&amp;linkCode=as2&amp;camp=247&amp;creative=7399&amp;creativeASIN=B000LPS54C">ディスクウォーリア4.0</a>を購入して修復を試みる価値はあると判断した．待つこと数時間，ディレクトリは再構築され，マウントすることができた．破損が深刻なためディレクトリの置き換え不可との診断なので，バックアップをとっているところである．助かった！