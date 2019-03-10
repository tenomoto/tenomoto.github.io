---
id: 552
title: OpenZFS on OS X
date: 2015-01-05T13:32:02+09:00
author: takeshi
layout: post
guid: https://www.enomosphere.net/?p=552
permalink: /2015/01/05/openzfs-on-os-x/
categories:
  - コンピュータ
tags:
  - Mac
  - ZFS
---
Mac Pro Early 2008に新しいディスクを4つ入れる。既にOSはSSDにあり，入れ替え前のディスクのバックアップは済んでいる。<!--more-->

<a href="https://openzfsonosx.org/">Open ZFS on OS X</a>からOpenZFS_on_OS_X_1.3.0.dmgをダウンロードする。Mountain Lionを使っているので，OpenZFS on OS X 1.3.0 Mountain Lionをダブルクリックしてインストール。
<h4>ZFS poolの作成</h4>
<a href="https://openzfsonosx.org/wiki/Zpool#Creating_a_pool">Wiki</a>を参考にzpoolを作る。ただし，mirrorではなくraidz。ディスクの名前は，事前に<code>diskutil list</code>で確認しておく。ZFS poolの名前はここではzpool0としている。オプションは，次のように設定。大文字小文字の区別はMac流にしない（casesensitivity=insensitive），iTunesなどが使えるようにNFD normalizationを使う（normalization=formD），アクセス日時の記録はしない（atime=off），圧縮する（compression=lz4）。
<pre>$ sudo zpool create -f -o ashift=12 -O casesensitivity=insensitive -O normalization=formD -O atime=off -O compression=lz4 zpool0 raidz disk1 disk2 disk3 disk4
</pre>
<h4>zpoolの状態確認</h4>
<pre>$ zpool status
</pre>
<h4>権限の変更</h4>
作成されたZFS poolに，誰でも書き込みができるように権限を変更する。
<pre>$ sudo chmod 777 /zpool0
</pre>
<h4>マウントポイントの変更</h4>
既定ではZFS poolの名前がボリューム名として使われるため，zpool0が<code>/</code>にマウントされる（<code>/zpool0</code>）。OS Xの流儀にするため，マウントポイントを変更する。
<pre>$ sudo zfs mountpoint=/Volumes/Zenith zpool0
</pre>
<h4>手動マウント</h4>
なんらかの理由でマウントされていないときは，手動でマウントできる。
<pre>$ sudo zfs mount zpool0</pre>
<h4>ディスクユーティリティ</h4>
OpenZFSをインストールすると，ディスクユーティリティでも，ZFSで初期化ができるようになる。