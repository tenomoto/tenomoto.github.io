---
id: 572
title: KUINS-III環境でselfupdateを可能にするMacPortsの設定
date: 2015-02-24T13:47:36+09:00
author: takeshi
layout: post
guid: https://www.enomosphere.net/?p=572
permalink: /2015/02/24/port-selfupdate-kuins3/
categories:
  - コンピュータ
tags:
  - macports
  - rsync
  - subversion
---
皆の役に立つわけではないが，KUNIS-III環境でのMacPortsの設定について書き留めておく。<!--more-->
<h3>1 ネットワーク環境設定</h3>
念のためシステムの設定を確認。

<a href="/wp-content/uploads/2015/02/network_preference.png"><img class="alignnone size-medium wp-image-574" src="/wp-content/uploads/2015/02/network_preference-300x260.png" alt="network_preference" width="300" height="260" /></a>
<ul>
	<li>「システム環境設定」&gt;「ネットワーク」で接続しているインターフェースを左から選択し，「詳細...」ボタンをクリック。</li>
	<li>「プロキシ」タブ上の「構成するプロトコロルを選択」中「自動プロキシ構成」をチェックし「プロキシ構成ファイル」URLに</li>
</ul>
<pre>http://wpad.kuins.net/proxy.pac</pre>
と入力し「OK」ボタンをクリックして設定。
<ul>
	<li>「適用」ボタンをクリックして有効化。</li>
</ul>
<h3>2 rsync</h3>
rsyncのプロキシを設定する。${prefix}/etc/macports/macports.confを編集。${prefix}の既定値は/opt/local。
<pre>proxy_rsync proxy.kuins.net:8080
</pre>
環境変数RSYNC_PROXYでもよいはずだがうまくいかない。port treeをrsyncで取得している場合は，これでselfupdateができるようになる。rsync接続が禁止されている場合は，ソースはSubversionを使って手動で取得する。
<h4>追記</h4>
環境変数でうまくいかなかったのは，sudoコマンドが環境変数を引き継がなかったため。
<pre>$ export RSYNC_PROXY=proxy.kuins.net:8080
$ sudo -E port selfupdate
</pre>
とするとうまくいった。
<h3>3 Subversion</h3>
${prefix}/etc/macports/sources.confを次のように設定すると，port treeをSubversionで取得するようになる。lognameはユーザ名。
<pre>#rsync://rsync.macports.org/release/tarballs/ports.tar [default]
file:///Users/logname/Macports/ports [default]
</pre>
/Users/logname/Macports/portsはport treeを次のsvnコマンドを使って手動で取得した場所。
<pre>$ mkdir -p /Users/logname/Macports/
$ cd /Users/logname/Macports/
$ svn co https://svn.macports.org/repository/macports/trunk/dports/ ports
</pre>
KUINS-IIIのようにhttpがプロキシ経由の場合は，Subversionのプロキシ設定が必要。設定は~/.subversion/serversの[global]セクションにする。portコマンドのホームディレクトリは/opt/local/var/macports/homeなので，/opt/local/var/macports/home/.subversion/serversにも同様に設定する。
<pre>http-proxy-host=proxy.kuins.net
http-proxy-port=8080
</pre>
<h4>追記</h4>
httpsでport treeを取得している場合は，さらに<a href="https://trac.macports.org/wiki/howto/SyncingWithSVN">設定</a>が必要。ただし，OSのsubversionではうまくいかない。MacPortsのsubversionをインストールする。