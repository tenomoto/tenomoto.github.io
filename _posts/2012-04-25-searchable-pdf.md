---
id: 57
title: 検索可能なPDF作成
date: 2012-04-25T16:03:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2012/04/25/%e6%a4%9c%e7%b4%a2%e5%8f%af%e8%83%bd%e3%81%aapdf%e4%bd%9c%e6%88%90/'
permalink: /2012/04/25/searchable-pdf/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2012/04/pdf.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/3346366420019955536
categories:
  - コンピュータ
tags:
  - macports
  - PDF
---
論文の多くがPDF化されているが、透明テキストがついていない場合がある。Acrobatがするのが楽だが、フリーウェアでも可能。

MacPortsでは、ghostscript, hocr2pdfが含まれているexact-image, tesseractと辞書 (tesseract-eng, tesseract-jpnなど) をインストールする。以下の手順をスクリプトにまとめた（参考にした<a href="http://optphys.sci.hokudai.ac.jp/~sekika/wiki/index.php?%B2%E8%C1%FCPDF%A4%CB%C6%A9%CC%C0%A5%C6%A5%AD%A5%B9%A5%C8%A4%F2%C5%BD%A4%EA%C9%D5%A4%B1">rubyスクリプト</a>）。

LZW圧縮してもファイルサイズ大きい3倍くらいになる。圧縮しないと10倍くらい。Acrobatだと元のファイルより小さくなっている。<span style="font-family: monospace; white-space: pre;">-dPDFSETTINGS=/screen</span>だと解像度はともかく、画像が乱れて使い物にならなかった。
<span style="font-family: monospace; white-space: pre;">
</span>
gsの-sDEVICE=tifflzwはモノクロなので、一旦非圧縮の24bitカラーに出力してからconvertで変換している。

追記: pdftkでまとめるのが良い。MacPortsではgcc-4.5のバグ?のため、コンパイルできないのでバイナリをインストール。サイズは<a href="https://www.enomosphere.net/2012/04/26/pdf%e3%81%ae%e5%9c%a7%e7%b8%ae/">pdfsizeopt</a>でAcrobat並みのサイズになった。
<ol>
 	<li>ghostscriptでPDFのページを分解してtiffにする。</li>
 	<li>tesseract-ocrでOCRしてhocr2pdf用のHTMLを作成。</li>
 	<li>convertでtiffをLZW圧縮。</li>
 	<li>hocr2pdfで透明テキストとLZW圧縮したtiffをまとめてPDFを作成。</li>
 	<li>pdftk<span style="text-decoration: line-through;">ghostscript</span>で一つのPDFにまとめる。</li>
</ol>
<pre>#!/bin/sh
PDFTK=pdftk
GS=gs
RES=300
TIFF=tiff24nc
GSOPTS="-q -dBATCH -dNOPAUSE"
TESSERACT=tesseract
CONVERT=convert
CONVERTOPTS="-compress lzw"
HOCR2PDF=hocr2pdf
PDFQUALITY=/ebook
if [ $# -lt 2 ]; then
  echo "Usage :: $0 input.pdf lang (eng|jpn)"
  exit
fi
FNAME=$1
LANG=$2
TMPDIR=`mktemp -d /tmp/pdfocr.XXXXXX`
cp "${FNAME}" ${TMPDIR}
cd ${TMPDIR}
${GS} ${GSOPTS} -r${RES}x${RES} -sDEVICE=${TIFF} -sOutputFile="${FNAME%.pdf}_%04d.tiff" "${FNAME}"
rm -f ${FNAME}
for tiff in *.tiff; do
  ${TESSERACT} -l ${LANG} ${tiff} ${tiff} hocr &gt; /dev/null 2&gt;&amp;1
  ${CONVERT} ${COVERTOPTS} ${tiff} ${tiff%.tiff}_lzw.tiff
  hocr2pdf -i ${tiff%.tiff}_lzw.tiff -o ${tiff%tiff}pdf &lt; ${tiff}.html
  rm -f ${tiff}.html
done</pre>
<pre>#${GS} ${GSOPTS} -sDEVICE=pdfwrite -dCompatibilityLevel=1.4 -dPDFSETTINGS=${PDFQUALITY} -sOutputFile="${OLDPWD}/${FNAME%.pdf}_ocr.pdf" `ls -1 *.pdf`
${PDFTK} *.pdf cat output ${OLDPWD}/${FNAME%.pdf}_ocr.pdf
cd -
rm -rf ${TMPDIR}</pre>