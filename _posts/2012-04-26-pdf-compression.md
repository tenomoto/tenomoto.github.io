---
id: 56
title: PDFの圧縮
date: 2012-04-26T17:22:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2012/04/26/pdf%e3%81%ae%e5%9c%a7%e7%b8%ae/'
permalink: /2012/04/26/pdf-compression/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2012/04/pdf_26.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/104740435512864979
categories:
  - コンピュータ
tags:
  - macports
  - PDF
---
## 2019/3/22追記

情報が古くなっいます。
[pdfsizeopt](https://github.com/pts/pdfsizeopt)に従ってインストールしてください。sam2pなども含まれています。
ただしあまり圧縮できませんでした。

macOSの場合は[Quartzフィルタ](/2019/03/22/quartz-filter/)を利用した方が良いです。

---

<a href="https://github.com/pts/pdfsizeopt">pdfsizeopt</a>でPDFの圧縮を試みる。

jbig2enc, sam2pをMacPortsからインストール。

pngoutとMultivalent.jarはオープンソースではない。pngoutはバイナリを~/local/binに置く。Multvalent.jarのToolsは現在のバージョンには含まれないので、pdfsizeoptのページからダウンロードして、~/Library/Java/Extensionsに置く。デフォルトでCLASSPATHに含まれるが、環境変数に含まれないのでpdfsizeopt.pyからは分らない。

pdfsizeoptをチェックアウト。pythonの在処を書き換えたpdfsizeopt.pyを~/local/libexecに置く。引数とCLASSPATHを渡し、大量の中間ファイルを取り除くために、pdfsizeopt.pyを下記のスクリプトから呼び出す。

サイズは確かに小さくなるが、処理に結構時間がかかる。途中で落ちてしまうこともある。pdftkでつなげた場合はうまくいった。
<pre>#!/bin/sh
PDFSIZEOPT=${HOME}/local/libexec/pdfsizeopt.py
OPTS="--use-pngout=true --use-jbig2=true --use-multivalent=true"
MULTIVALENT=${HOME}/Library/Java/Extensions/Multivalent.jar
if [ $# -lt 1 ]; then
  echo "usage :: $0 input.pdf"
  exit
fi
INPUT=$1
TMPDIR=`mktemp -d /tmp/pdfsizeopt.XXXXXX`
cp ${INPUT} ${TMPDIR}
cd ${TMPDIR}
CLASSPATH=${MULTIVALENT} ${PDFSIZEOPT} ${OPTS} ${INPUT}
mv ${INPUT%pdf}psom.pdf ${OLDPWD}
rm -rf ${TMPDIR}</pre>
