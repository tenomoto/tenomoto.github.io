---
id: 610
title: Yosemiteで論理ボリュームを削除
date: 2016-03-25T16:22:18+09:00
author: takeshi
layout: post
guid: https://www.enomosphere.net/?p=610
permalink: /2016/03/25/yosemite-logical-volume/
categories:
  - コンピュータ
tags:
  - CoreStorage
  - Mac
---
Mac Pro (Early 2008)に4つの6TBハードディスクが内蔵して使っている。<a href="https://openzfsonosx.org">OpenZFS</a>を使っていたのだが，Yosemiteでは不安定な上に，以下を試したがSpotlightが有効にならない。
<!--more-->

<ul>
	<li>mdutil -i on ボリューム名</li>
	<li>zpool/zfs upgrade</li>
	<li>defaults write com.apple.desktopservices DSDontWriteNetworkStores false</li>
</ul>
あきらめてRAID10を構成することにした。中身はバックアップのある壊れてもよいものだったので，ディスクを消去した。その結果，ディスクごとにCoreStorageの論理ボリューム（logical volume）が作成されてしまった。YosemiteでCoreStorageは既定のようである。

diskutil cs revertで<a href="http://www.macotakara.jp/blog/mac_os_x/entry-25055.html">解除できる</a>とのことだが，diskutil cs listを見るとRevertible: Noとなっており戻すことはできない。

diskutil csには，<a href="http://blog.fosketts.net/2011/08/05/undocumented-corestorage-commands/">マニュアルに記述されていないコマンド</a>がある。このうちremoveDiskを試したところ，物理ボリュームに戻った。この際，初期化が行われ論理ボリュームにあったファイルは消えてしまった。
<pre>$ diskutil list
$ diskutil eject disk番号
$ diskutil cs list
$ sudo diskutil cs removeDisk 物理ボリュームのUUID
</pre>