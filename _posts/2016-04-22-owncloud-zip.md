---
id: 629
title: ownCloudからダウンロードしたzipファイルの解凍
date: 2016-04-22T11:38:30+09:00
author: takeshi
layout: post
guid: https://www.enomosphere.net/?p=629
permalink: /2016/04/22/owncloud-zip/
categories:
  - コンピュータ
tags:
  - Mac
  - macports
  - クラウド
---
<a href="https://owncloud.org">ownCloud</a>は自前でファイル共有サーバを立てるためのサーバアプリケーション。フォルダをまとめてダウンロードしたところ，Macでzipの解凍ができない。<!--more-->

検索してみるとよく知られた問題のようである。ownCloudは大容量データをアーカイブするためにzip64を導入したが，Macのアーカイブユーティリティが対応していない。<code>/usr/bin/unzip</code>は古いバージョンだ。
<pre>$ /usr/bin/unzip --version
caution:  both -n and -o specified; ignoring -o
UnZip 5.52 of 28 February 2005, by Info-ZIP.  Maintained by C. Spieler.  Send
bug reports using http://www.info-zip.org/zip-bug.html; see README for details.
</pre>
Info-ZIPの<a href="http://www.info-zip.org/UnZip.html">UnZipのページ</a>にはセキュリティ上の脆弱性が警告されている。新しいものを入れた方が良さそうだ。<code>unzip</code>と<code>zip</code>を<a href="http://www.macports.org/">MacPorts</a>でインストールする。
<pre>$ sudo port -d install unzip zip
</pre>
MacPortsで入れたunzipで解凍しようとしたが，複数の部分（multi-part）からなるアーカイブだとする警告が出て解凍できない。
<pre>Archive:  archive.zip
warning [archive.zip]:  zipfile claims to be last disk of a multi-part archive;
  attempting to process anyway, assuming all parts have been concatenated
  together in order.  Expect "errors" and warnings...true multi-part support
  doesn't exist yet (coming soon).
</pre>
実際は単一のファイルしかない。<code>zip</code>で修復する。
<pre>$ zip -F archive.zip --out archive1.zip
</pre>
修復したファイルも解凍できない。
<pre>Archive:  archive1.zip
   skipping: archive1/               need PK compat. v4.5 (can do v2.1)
   skipping: archive1/file1.docx  need PK compat. v4.5 (can do v2.1)
   skipping: archive1/file2.docx  need PK compat. v4.5 (can do v2.1)
</pre>
圧縮アリゴリズムは7zipのようである。MacPortsで<code>p7zip</code>をインストールし，<code>7z</code>で解凍する。
<pre>$ sudo port -d install p7zip
$ 7z x archive1.zip 
</pre>
<code>7z</code>では解凍できた。試しに元のファイルを解凍してみたら，解凍できた。
<pre>$ 7z x archive.zip 
</pre>
結論。ownCloudでダウンロードしたアーカイブの拡張子は<code>zip</code>だが，7zip形式で圧縮されているので，<code>p7zip</code>をインストールすれば<code>7z</code>で解凍できる。