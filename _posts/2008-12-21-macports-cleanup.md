---
id: 158
title: MacPortsの大掃除
date: 2008-12-21T09:08:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2008/12/21/macports%e3%81%ae%e5%a4%a7%e6%8e%83%e9%99%a4/'
permalink: /2008/12/21/macports-cleanup/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2008/12/macports.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/3532186556549761004
categories:
  - コンピュータ
tags:
  - macports
---
MacPortsのパッケージは，コミッタ，パッケージ管理者そしてユーザ有志の努力により，絶えず更新が続いている．

インストールされているものがパッケージよりも古くなったものの一覧は
<pre>port outdated</pre>
とすると表示される．

MacPortsのパッケージを更新するときのコマンドはport upgradeである．特定のパッケージfooを更新するには，
<pre>sudo port upgrade foo</pre>
とする．すべてを更新するには，
<pre>sudo port upgrade outdated</pre>
とする．upgradeをする前に
<pre>sudo port sync</pre>
をして，ソースツリーを更新しておく．

更新したパッケージやそれに依存するパッケージなど旧バージョンはdeactivateされ消されずに残る．更新をするたびに「ごみ」がたまっていく．既定で古いものを残すようにしているのは，新しいパッケージが動くことを確認してから古いものを消せばよいからである．
<pre>port -u uninstall</pre>
とすると「ごみ」をすべて清掃してくれる．古いものを残す必要がないときは，
<pre>port -u upgrade foo</pre>
とすると旧バージョンは消去される．更新対象のfooは，最上位に位置する「大物」だと依存するライブラリも更新され，-u付きの場合は古いものが消去されるので楽である．