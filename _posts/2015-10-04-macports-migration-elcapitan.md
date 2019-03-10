---
id: 596
title: OS X El CapitanにアップグレードしたのでMacPortsを入れ直し
date: 2015-10-04T11:29:32+09:00
author: takeshi
layout: post
guid: https://www.enomosphere.net/?p=596
permalink: /2015/10/04/macports-migration-elcapitan/
categories:
  - コンピュータ
tags:
  - Mac
  - macports
---
MacPortsは，OSのバージョンを上げたら入れ直し（migration）が必要。OS X El Capitanにアップグレードしたので，MacPortsを入れ直す。
<!--more-->

<h3>1.　はじめに</h3>
El Capitanにアップグレードしたマシンでportコマンドを実行すると，
<pre>$ ~ takeshi$ sudo port -d selfupdate

Password:

Error: Current platform "darwin 15" does not match expected platform "darwin 14"

Error: If you upgraded your OS, please follow the migration instructions: https://trac.macports.org/wiki/Migration

OS platform mismatch
</pre>
のようにエラーが出る。エラーメッセージにあるように，<a href="https://trac.macports.org/wiki/Migration">Migration</a>に従って入れ直す必要がある。

ただし，各パッケージのバイナリをビルドするサーバ（buildbot）が稼働していないので，バイナリはまだ提供されていない。選択肢は3つ。
<ol>
	<li>充分時間をとって，ソースからコンパイルする。コンパイルに問題があるパッケージは，<a href="https://trac.macports.org/wiki/ElCapitanProblems">ElCapitanProblems</a>に掲載され始めている。掲載されていないものの中にもうまくいかないものがあるかもしれない。</li>
	<li>YosemiteでインストールしたMacPortsをそのまま使い続ける。ほとんどはそのまま動くはずだ。ただし，OSのライブラリに動的にリンクされているものがあれば，ライブラリのバージョンが変わったり，ライブラリが無くなったりすると，動作しない可能性もある。portコマンドはOSのバージョンが違うとエラーを出すようになっているので，port treeの更新も新しいパッケージの導入もできない。</li>
	<li>El Capitanへのアップグレードをもう少し後にする。El Capitanにアップグレードすると，動かなくなるソフトウェアが出て仕事にならなくなる可能性がある。メインのマシンのEl Capitanへのアップグレードは慎重に検討してからの方がよい。</li>
</ol>
職場のメインのマシンは，しばらくYosemiteのままにする。MacPortsのメンテナ・コミッタをしているので，El Capitanを試す必要がある。そこで自宅のマシンをEl Capitanにアップグレードした。iPhoneやiPadのOSをiOS 9にしたので，El Capitanのメモを使えるようにしたかったのもアップグレードの理由だ。
<h3>2. 準備</h3>
El Capitanの登場に合わせて，<a href="https://twitter.com/macports/status/649688548480806912">MacPorts 2.3.4がリリース</a>された。既にEl Capitan用のpkgインストーラが<a href="https://www.macports.org/install.php">Installation</a>ページに用意されているが，ここではsvnから<a href="https://svn.macports.org/repository/macports/tags/release_2_3_4/base/">release 2.3.4</a>を取得してソースからコンパイルする。<a href="https://www.macports.org/install.php">Installation</a>ページに説明されているように，XcodeをApp Storeから取得してライセンスを読んで，agree（とタイプする）しておく必要がある。
<pre>$ sudo xcodebuild -license</pre>
Xcode Betaを試したりして，複数のXcodeがある場合は，
<pre>$ sudo xcode-select -print-path</pre>
で確認し，必要に応じて
<pre>$ sudo xcode-select -switch /Applications/Xcode.app/Contents/Developer</pre>
などとする。
<h3>3. 入れ直し</h3>
<h4>3.1 MacPorts 2.3.4のインストール</h4>
MacPorts関連のファイルはホームの~/MacPortsに入れているので，そこに移動して作業開始。
<pre>$ cd ~/MacPorts</pre>
svnでリリース2.3.4を取得し，コンパイルの後，インストール。
<pre>$ svn co https://svn.macports.org/repository/macports/tags/release_2_3_4/base/ base_2_3_4
$ cd base_2_3_4
$./configure &amp;&amp; make
sudo make install
</pre>
これでportコマンドが動作するようになった。MacPortsとport treeを更新。
<pre>sudo port -d self update</pre>
<h4>3.2 入れ直し作業</h4>
後は<a href="https://trac.macports.org/wiki/Migration">Migration</a>に従って作業する。まずはインストールされているものの一覧を書き出す。
<pre class="wiki">$ port -qv installed &gt; myports_yosemite.txt</pre>
ユーザがリクエストした（明示的にインストールを指示した）portの一覧を書き出す。
<pre class="wiki">$ port echo requested | cut -d ' ' -f 1 &gt; requested_yosemite.txt</pre>
インストールされているportを全てuninstallする。
<pre class="wiki">$ sudo port -f uninstall installed</pre>
念のためビルドの残骸を削除する。
<pre class="wiki">$ sudo rm -rf /opt/local/var/macports/build/*</pre>
インストールされていたportを復元するTclスクリプトをダウンロードする。ここでは~/MacPorts/binに格納している。
<pre class="wiki">$ cd bin
$ curl -O https://svn.macports.org/repository/macports/contrib/restore_ports/restore_ports.tcl
$ chmod +x restore_ports.tcl
$ cd ..
$ sudo bin/restore_ports.tcl myports_yosemite.txt</pre>
リクエストの状態を復元する。
<pre class="wiki">$ sudo port unsetrequested installed
$ xargs sudo port setrequested &lt; requested_yosemite.txt</pre>

jason より:	

2015年12月16日 5:06 PM

非常に助かりました。今は、Migrationをしている最中….

ピンバック: [【Mac OSX】El CapitanでMacPortsをインストール |](http://atomicbox.tank.jp/developer/1226/)

## 「OS X El CapitanにアップグレードしたのでMacPortsを入れ直し」への2件のフィードバック

### jason より:	

2015年12月16日 5:06 PM

非常に助かりました。今は、Migrationをしている最中….
