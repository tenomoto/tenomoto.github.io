---
id: 99
title: Time Capsule導入
date: 2010-03-08T22:17:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2010/03/08/time-capsule%e5%b0%8e%e5%85%a5/'
permalink: /2010/03/08/time-capsule/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2010/03/time-capsule.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/3378065512143994689
categories:
  - コンピュータ
tags:
  - Mac
  - Time Capsule
---
Amazonで<a href="http://www.amazon.co.jp/gp/product/B002TOJU10?ie=UTF8&amp;tag=enomospheddoj-22&amp;linkCode=as2&amp;camp=247&amp;creative=7399&amp;creativeASIN=B002TOJU10">APPLE Time Capsule 2TB MC344J/A</a>を購入．

自作PCの外付HDDでのTime Machineには成功したが，PCとHDDの電源を入れっぱなしにしておくことには抵抗がある．

サードパーティのNASでもTime Machineは可能だし，NAS対応のケースに安価なバルクHDDを入れても良い．実際PCにつないだのは，<a href="http://www.amazon.co.jp/gp/product/B00104EQQY?ie=UTF8&amp;tag=enomospheddoj-22&amp;linkCode=as2&amp;camp=247&amp;creative=7399&amp;creativeASIN=B00104EQQY">ロジテック クレードルタイプ HDDリーダーライタ eSATA&amp;USB2.0接続タイプ LHR-DS01SAU2</a>.

<a href="http://www.amazon.co.jp/gp/product/B002TOJHAE?ie=UTF8&amp;tag=enomospheddoj-22&amp;linkCode=as2&amp;camp=247&amp;creative=7399&amp;creativeASIN=B002TOJHAE">Apple AirMac Extremeベースステーション MC340J/A</a>に，現在使っているハードディスクをNASケースに入れてつなごうと考えた.

電源内蔵のハードディスクケースは現在製造物責任法のため，手に入りにくいようだ．しかも安いとはいえない.

Time Capsuleは割高だと言われているが，無線LAN, ギガビットの有線ハブ (3つ), 2TBハードディスク，電源内蔵ハードディスクと考えると決して高くないように思われる.

Ethernetケーブルと電源をつなぐとAirMacユーティリティがTime Capsuleを自動的に検出. AirMacユーティリティの更新を求められる. 添付のCDからイントールすると，1) 新たなネットワークを作るか, 2) 既存の無線LANを置き換えるか, 3) 既存の無線LANに接続するか聞かれる. プロパイダから借りているルータに差している無線LANカードを置き換えるので, 2) に該当. 無線LANカードを抜くと, 設定がすべて引き継がれている. すばらしい.

いったんTime Machineの設定は後回しにしたが, 後で有線で接続し, Time CapsuleのDataを選択してバックアップ実行.

なお，比較的最近 (2010/2/28) 付のユーザーレビューで最悪との評がある.
買ったばかりなので分からないが, <a href="http://timecapsuledead.org/closed.html">旧製品の問題</a>はアップルが対応している. また有線がギガビットでないことで躊躇したとのコメントも目にしたが，現在の製品はWANx1, LANx3ポートすべてギガビットになっている．新旧製品の情報が入り乱れているので注意．