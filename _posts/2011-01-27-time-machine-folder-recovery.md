---
id: 74
title: Time Machineからフォルダが復元できない
date: 2011-01-27T09:27:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2011/01/27/time-machine%e3%81%8b%e3%82%89%e3%83%95%e3%82%a9%e3%83%ab%e3%83%80%e3%81%8c%e5%be%a9%e5%85%83%e3%81%a7%e3%81%8d%e3%81%aa%e3%81%84/'
permalink: /2011/01/27/time-machine-folder-recovery/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2011/01/time-machine.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/3492016813984697501
categories:
  - コンピュータ
tags:
  - Mac
  - Time Machine
---
毎日送られてくる迷惑メール一覧をまとめて消そうと思い，Command+Aで選択したら全ての選択されていて，全てのメッセージがゴミ箱に行きなった．

整理せず「受信」に全てためているので，25,000件くらい．ゴミ箱への移動も時間がかかる．移動を待って元に戻せば良かったのだが，短気をおこして止めようとしたのがいけなかった．Mailを強制終了することになり，ゴミ箱にある1か月以上前のメッセージは再び立ち上げたときに消されてしまった．

Time Machineがあるじゃないか．

ところが，復元したはずの~/Library/Mailは空．Finderでコピーしても同様．ファイルは復元されるがフォルダ（ディレクトリ）は復元されない．

Time MachineのGUIを使わずに
<pre>
tar cf - | (cd 保存先; tar xvf -)</pre>
しても特殊なハードリンク (Archive Directory Link)がコピーされるだけで実体ではない．

試行錯誤の結果，別のマシンにTime Machineに使っているディスクをマウントしたところ，フォルダを復元できた．Finderでコピーしても，DockのTime Machineアイコンを長押しするか右クリックして「ほかのTime Machineディスクをブラウズ...」を選んでGUIを使ってもできた．